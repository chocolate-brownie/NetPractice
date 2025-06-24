# NetPractice Notes

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
