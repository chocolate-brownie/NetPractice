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

### What is the key difference between a switch and a router?

**Switch** can connects your all local hosts together to communicate with each other while the **Router** opens up doors to connect to other hosts in other neighborhoods (subnet masks)

---
---

### The One Universal Method That Always Works: The Binary Method

The one single method that never changes is based on counting the `1`s and `0`s in the subnet mask's binary code.

Let's break down the two things you want to calculate:
1.  The **Number of Available Hosts**.
2.  The **Network Ranges** (the "blocks" or "neighborhoods").

#### **1. How to Calculate the NUMBER OF HOSTS (Your First Method Was Correct!)**

Your original method was the **correct and universal way** to find the number of hosts. It never changes.

* **Step 1:** Convert the entire subnet mask to its 32-bit binary form.
* **Step 2:** Count the total number of zeros (`n`).
* **Step 3:** The number of usable hosts is **always** $2^n - 2$.

Let's test this on all our examples:
* **`255.255.255.192`**: `...11000000`. Has **6 zeros**.
  * Usable Hosts = $2^6 - 2 = 64 - 2 = 62$.
* **`255.255.255.224`**: `...11100000`. Has **5 zeros**.
  * Usable Hosts = $2^5 - 2 = 32 - 2 = 30$.
* **`255.255.192.0`**: `...11000000.00000000`. Has **14 zeros** (6 in the 3rd block + 8 in the 4th).
  * Usable Hosts = $2^{14} - 2 = 16384 - 2 = 16382$.

This method is universal. It always works for finding the host count.

#### **2. How to Calculate the NETWORK RANGES (The "Magic Number" Shortcut)**

Now, let's talk about the `256 - x` calculation.

**This method is NOT for finding the number of hosts.** This is a shortcut to find the **block size** of your networks, which helps you find the starting and ending addresses of each range.

* **Step 1:** Find the "interesting octet" (the first one that isn't `255`).
* **Step 2:** Calculate the block size: `256 - interesting_number`.
* **Step 3:** List the multiples of that block size to find the start of each network.

**Why did this seem like a way to find the number of hosts?**
Because when the interesting octet is the **last one**, the block size (`32`) is very close to the number of usable hosts (`30`). The block size is the total addresses in the block ($2^n$), and the usable hosts is that number minus 2.

### The Single, Unified Workflow

So, here is the one proper way to think about it, which combines both ideas:

1.  **To find the number of hosts:** Use your original binary method. Convert the mask, count the total zeros (`n`), and calculate $2^n - 2$. This is the only way.

2.  **To find the specific IP ranges:** Use the "magic number" shortcut. Find the interesting octet, calculate `256 - x` to get the block size, and then map out your networks (`.0, .32, .64, etc.`).

You were not wrong. Your first method was the correct one for the question you were asking ("how many hosts?"). The "magic number" method answers a different question ("where do my network ranges start?"). I apologize for not making that distinction clearer earlier.

---
---
## Setting up **Default Gateway**

### The Two Questions Your Computer Asks

**Question 1: "Is the final destination on my local network?"**

Your computer looks at the destination IP (`8.8.8.8`) and compares it to its own IP address and subnet mask (e.g., `192.168.1.10` with mask `255.255.255.0`). It does the math and realizes that `8.8.8.8` is **NOT** a local neighbor. It's on a remote network far away.

The answer to Question 1 is **NO**.

This leads directly to the second and most important question.

**Question 2: "Since the destination is remote, do I have a Default Gateway configured?"**

Your computer now looks at its own network settings for the "Default Gateway" field.

* **Scenario A: The Gateway is NOT configured.** If the gateway field is empty, the process stops. Your computer has no idea what to do with the packet and discards it. You will get an error like "No route to host." The journey is over before it began.

* **Scenario B: The Gateway IS configured.** Your computer sees that its Default Gateway is set to `192.168.1.1` (the router's local IP). The answer to Question 2 is **YES**. Now, your computer knows exactly what to do.

### The Action: How the Packet Gets to the Gateway

This is the deeper part. Your computer now knows it needs to send the packet to the gateway (`192.168.1.1`), but how does it physically do that on the local network?

It uses a process called **Address Resolution Protocol (ARP)**.

1.  **The Problem:** On a local network, devices use physical hardware addresses (called **MAC addresses**) to deliver data, not IP addresses. An IP address is like a person's name, while a MAC address is like their unique fingerprint. Your computer needs to find the *fingerprint* of its gateway.

2.  **The ARP "Shout":** Your computer broadcasts a message onto the local network created by the switch. This ARP message effectively shouts: **"WHO HAS THE IP ADDRESS `192.168.1.1`? PLEASE TELL ME YOUR MAC ADDRESS!"**

3.  **The Reply:** Every device on the local network hears this shout. Other computers and printers ignore it. But the router's interface recognizes its own IP address and sends a reply directly back to your computer: **"I have `192.168.1.1`. My MAC address is AA:BB:CC:11:22:33."**

4.  **The Delivery:** Your computer now knows the physical MAC address of its gateway. It takes the original data packet (which is still addressed to the final destination `8.8.8.8`) and puts it inside an "envelope" (an Ethernet frame) addressed to the router's MAC address. The switch sees this envelope and delivers it directly to the router.

### The Final Step: The Router's Job

Once the router receives the packet, its job begins. It "unwraps" the envelope, looks at the packet's final destination (`8.8.8.8`), checks its own massive routing table (its map of the internet), and forwards the packet on its next hop toward Google.

This entire process is why the gateway **must** be local. If you set the gateway to a remote IP, your computer's ARP "shout" for that remote IP would go unanswered on the local network, and it would never be able to send the packet.

---
---

### **Simple Note: How to Find a Network Address**

**Goal:** To find the starting address (the Network Address) of the subnet that a specific computer belongs to.

**What You Need:**
1.  The computer's IP Address: `92.181.11.227`
2.  The computer's Subnet Mask: `255.255.255.128`

#### **Step 1: Find the "Magic Number" from the Subnet Mask.**
Look at the part of the mask that is not `255`. In this case, it is `.128`.

Subtract this number from 256.
`256 - 128 = 128`
The Magic Number (or block size) is **128**.

#### **Step 2: List the starting points of the network blocks.**
The blocks will be multiples of the magic number (128). The possible starting points are:
* `0`
* `128`

#### **Step 3: Find which block your computer's IP lives in.**
Look at the last number of your computer's IP address, which is `.227`.

Ask the question: "Which block does `227` fall into?"
* Is it between 0 and 127? No.
* Is it between 128 and 255? **Yes.**

This means your computer lives in the network block that starts at `128`.

#### **Result:**
The starting number of the block is the Network Address.

* The Network Address is: **`92.181.11.128`**
* We add the CIDR mask (`/25`) to describe the size of the network fully: **`92.181.11.128/25`**
