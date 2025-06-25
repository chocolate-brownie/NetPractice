# NetPractice Notes

Here is a list of the most common IPv4 subnet masks, their CIDR notation, and how many devices (hosts) they can support.

### Common IPv4 Subnet Mask Ranges

| Subnet Mask | CIDR Prefix | Usable Hosts | Common Use Case |
| :--- | :--- | :--- | :--- |
| **`255.0.0.0`** | `/8` | 16,777,214 | Very large corporate or ISP networks (e.g., the `10.0.0.0/8` private range). |
| **`255.255.0.0`** | `/16` | 65,534 | Large to medium-sized corporate or university networks. |
| **`255.255.240.0`** | `/20` | 4,094 | Medium-sized networks, often a block assigned to a company. |
| **`255.255.255.0`** | `/24` | 254 | **The most common mask.** Perfect for small office or home networks. |
| **`255.255.255.128`**| `/25` | 126 | Dividing a `/24` network into two smaller subnets. |
| **`255.255.255.192`**| `/26` | 62 | Creating four smaller networks from a `/24`, good for department separation. |
| **`255.255.255.224`**| `/27` | 30 | Smaller subnets for specific server groups or labs (like in your exercise). |
| **`255.255.255.240`**| `/28` | 14 | Small networks, often for a specific application or service. |
| **`255.255.255.248`**| `/29` | 6 | Very small networks, often used for the link between routers. |
| **`255.255.255.252`**| `/30` | 2 | **Point-to-Point links.** The most common choice for connecting exactly two devices, usually two routers. |
| **`255.255.255.254`**| `/31` | 2 | A special case for point-to-point links that conserves IP addresses (less common but very efficient). |
| **`255.255.255.255`**| `/32` | 1 | Represents a single, specific host. Often used in routing tables or firewall rules to identify one computer. |

**Key takeaway:** As the CIDR number (`/x`) gets bigger, the number of usable hosts gets smaller because more bits are being used for the network portion of the address. Noting down the `/24`, `/27`, and `/30` masks will be especially helpful for your NetPractice project.

---
---

Here are the most important reserved IPv4 address ranges you should not use for assigning to regular hosts on a public network:

### 1. Private Network Addresses
These ranges are reserved for use in private networks (like your home, school, or office). Internet routers do not forward traffic coming from these addresses. You will use these constantly in your exercises and career.

| Range Name | Address Range | Largest CIDR Block | Total Addresses |
| --- | --- | --- | --- |
| 24-bit block | `10.0.0.0` – `10.255.255.255` | `10.0.0.0/8` | ~16.7 million |
| 20-bit block | `172.16.0.0` – `172.31.255.255` | `172.16.0.0/12` | ~1 million |
| 16-bit block | `192.168.0.0` – `192.168.255.255`| `192.168.0.0/16` | 65,536 |

### 2. Loopback Address
This is the `127.0.0.0/8` block you encountered. A device uses this range to send network traffic to itself. You cannot use it to communicate between two different computers.

* **Range:** `127.0.0.0` – `127.255.255.255`
* **Commonly Used:** `127.0.0.1` is famously known as "localhost".

### 3. Link-Local Addresses (APIPA)
This range is used when a device is configured to get an address automatically (via DHCP) but cannot find a DHCP server. The device assigns itself an address in this range to communicate with other devices on the same local link.

* **Range:** `169.254.0.0` – `169.254.255.255` (`169.254.0.0/16`)

### 4. Multicast Addresses
This large block is used to send a single packet to multiple destinations simultaneously, essential for applications like streaming video or online gaming. You should never assign an address from this range to a single device interface.

* **Range:** `224.0.0.0` – `239.255.255.255` (`224.0.0.0/4`)

### 5. Documentation & Test Networks
IANA has reserved specific blocks of addresses to be used in examples and documentation (like this one!). This ensures that technical writers and educators don't accidentally use a real, public IP address in their examples.

* **TEST-NET-1:** `192.0.2.0` – `192.0.2.255` (`192.0.2.0/24`)
* **TEST-NET-2:** `198.51.100.0` – `198.51.100.255` (`198.51.100.0/24`)
* **TEST-NET-3:** `203.0.113.0` – `203.0.113.255` (`203.0.113.0/24`)

### 6. Other Special Use Ranges

* **"This" Network (`0.0.0.0/8`):** Reserved for representing the current, local network. `0.0.0.0` itself often means "any IPv4 address".
* **Carrier-Grade NAT (`100.64.0.0/10`):** Used by internet service providers when they run out of public IP addresses and need to share them among many customers.
* **Reserved for Future Use (`240.0.0.0/4`):** This block is set aside for potential future applications.
* **Limited Broadcast (`255.255.255.255`):** A special broadcast address for the local network segment.

---
---

# What is the key difference between a switch and a router?

**Switch** can connects your all local hosts together to communicate with each other while the **Router** opens up doors to connect to other hosts in other neighborhoods (subnet masks)
