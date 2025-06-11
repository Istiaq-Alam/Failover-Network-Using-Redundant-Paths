# :repeat: **What is MHSRP?**

MHSRP allows you to configure multiple HSRP groups on the same interface, enabling load balancing and redundancy. Each router is **Active** for one group and **Standby** for the other.

---

# :brain: ** Setup:**

* Network: `192.168.1.0/24`
* Router1: `192.168.1.1`
* Router2: `192.168.1.2`
* Virtual IPs:

  * Group 1: `192.168.1.254` (Active on Router1)
  * Group 2: `192.168.1.253` (Active on Router2)

---

# :white_check_mark: Step-by-Step MHSRP Configuration

---

## :wrench: **Router1 Configuration**

```bash
enable
configure terminal
interface fa0/0
  ip address 192.168.1.1 255.255.255.0

  standby 1 ip 192.168.1.254
  standby 1 priority 110
  standby 1 preempt

  standby 2 ip 192.168.1.253
  standby 2 priority 90
  standby 2 preempt
no sh

exit
 wr
```

---

## :wrench: **Router2 Configuration**

```bash
enable
configure terminal
interface fa0/0
  ip address 192.168.1.2 255.255.255.0

  standby 1 ip 192.168.1.254
  standby 1 priority 90
  standby 1 preempt

  standby 2 ip 192.168.1.253
  standby 2 priority 110
  standby 2 preempt
no sh

exit
  wr
```

---

## :wrench: **Switch Configuration**

Just make sure the switch interfaces connected to both routers and all PCs are up and on the same VLAN (e.g., VLAN 1 if default).

## :wrench: Switch0 -
```bash
enable
configure terminal

! Configure all PC ports on VLAN 1 (default)
interface range fa0/1 - fa5/1
 switchport mode access
 switchport access vlan 1

! Connection to Router1
interface fa0/1
 switchport mode access
 switchport access vlan 1

! Connection to Switch2 (trunk link)
interface fa2/1
 switchport mode trunk

exit
 copy running-config startup-config
```

---

## :wrench: Switch1 -
```bash
enable
configure terminal

! Configure all PC ports on VLAN 1 (default)
interface range fa0/1 - fa7/1
 switchport mode access
 switchport access vlan 1

! Connection to Router2
interface fa0/1
 switchport mode access
 switchport access vlan 1

! Connection to Switch1 (trunk link)
interface fa2/1
 switchport mode trunk

exit
 copy running-config startup-config
```

---

## :computer: **PC Configuration (Example for All PCs)**

Set **Default Gateway** based on the virtual IP that matches the HSRP group.

* For PCs on the left (e.g., PC4 to PC8):
  IP: `192.168.1.X`
  Subnet Mask: `255.255.255.0`
  Gateway: `192.168.1.253` (Router0’s group)

* For PCs on the right (e.g., PC5 to PC11):
  IP: `192.168.1.X`
  Subnet Mask: `255.255.255.0`
  Gateway: `192.168.1.254` (Router1’s group)

---

## :white_check_mark: **Test Failover**

* Turn off **Router1**, check if **Router2** takes over for Group 1 (VIP: `192.168.1.253`).
* Turn off **Router2**, check if **Router1** takes over for Group 2 (VIP: `192.168.1.254`).
* Ping across the network from different PCs and observe.

---