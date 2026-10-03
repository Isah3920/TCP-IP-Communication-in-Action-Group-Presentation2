# TCP/IP Communication in Action: Opening a Secure Website

**Course:** WADF105  
**Group:** TEAM-04  
**Programme:** FCDF-COHORT-11  
**Level:** 1, Semester 1  
**Presentation Date:** 30 September 2026  
**Presenters:** Isa Sani Alhassan (C11/26/FCDF17171) and Lelah Naomie (C11/26/FCDF17184)  
**On behalf of:** TEAM-04

---

## 1. Executive Summary

Opening a secure web page looks like a single action to the user, but it activates every layer of the TCP/IP stack, from DNS name resolution through to HTTPS encryption.

This report follows one request, where a user opens `https://example.com` on a laptop, from the client to the web server and back. Along the way, it explains the TCP/IP layers, how they compare with the OSI model, the four kinds of address involved, and the path a packet takes across the network.

---

## 2. The Scenario

A user opens:

> **https://example.com**

The request is traced from the client to the web server, and the response is traced back to the client.

### Protocols and Concepts Covered

- DNS
- TCP
- TLS
- HTTP
- IP
- MAC addressing
- Port numbers
- Network security

### Devices on the Path

1. Client laptop
2. Access point / switch
3. Router
4. Internet
5. Firewall
6. Web server

**Key point:** A single page load activates the complete TCP/IP stack.

---

## 3. The TCP/IP Model

The TCP/IP model has four layers. Each layer adds its own header to the data as it moves down the stack. This process is called **encapsulation**, and the unit of data, known as the **Protocol Data Unit (PDU)**, changes its name at each layer.

| # | Layer | Data Unit (PDU) | Role | Example Protocols |
|---|---|---|---|---|
| 1 | Application | Message | Provides services to the user | HTTP, DNS, TLS |
| 2 | Transport | Segment | Provides end-to-end delivery, ports, and reliability | TCP, UDP |
| 3 | Internet | Packet | Provides logical addressing and routing | IP |
| 4 | Network Access | Frame | Handles physical transmission on the local link | Ethernet, Wi-Fi, ARP |

Reading downward through the TCP/IP stack, the data changes form as each lower layer wraps it with the information required to move the request across the network.

### Encapsulation

When the request leaves the application and moves down the TCP/IP stack, each layer adds information needed for communication:

**Application data → TCP segment → IP packet → Network frame**

At the destination, the reverse process occurs. This is called **de-encapsulation**, where each layer removes and processes the information added by the corresponding layer.

---

## 4. TCP/IP Versus OSI

The TCP/IP model and the OSI model describe network communication using layers. However, the two models organize these functions differently.

### Comparison

| OSI Model (7 Layers) | TCP/IP Model (4 Layers) | Purpose |
|---|---|---|
| 7. Application | Application | User-facing network services such as HTTP and DNS |
| 6. Presentation | Application | Data representation and encryption-related functions such as TLS |
| 5. Session | Application | Establishing and managing communication sessions |
| 4. Transport | Transport | TCP port numbers, reliability, and end-to-end delivery |
| 3. Network | Internet | IP addressing and routing |
| 2. Data Link | Network Access | MAC addressing and local network frames |
| 1. Physical | Network Access | Physical transmission using Ethernet or Wi-Fi |

The most important difference is at the top of the models. The OSI model separates the **Application, Presentation, and Session** layers, while the TCP/IP model generally combines their functions into a single **Application layer**.

---

## 5. Four Kinds of Address

Four different types of addressing work together to help deliver traffic from the laptop to the web server. Each has a different purpose and scope.

| Address Type | Example | What It Does |
|---|---|---|
| URL / FQDN | `https://example.com` | Provides the human-readable name used to identify the website. DNS resolves the domain name to an IP address. |
| IP Address | `192.168.1.10 → 93.184.216.34` | Provides logical addressing and allows traffic to be routed between networks. |
| MAC Address | `aa:bb:cc:11:22:33 → router MAC` | Provides local delivery on the current network link. |
| Port Number | `54321 → 443` | Identifies the application/service involved in the communication. HTTPS commonly uses port 443. |

### How the Addresses Fit Together

The four addressing concepts work together as follows:

1. **URL/FQDN** provides the human-readable website name.
2. **DNS** resolves the domain name into an IP address.
3. **IP addressing** allows packets to be routed between different networks.
4. **MAC addressing** handles delivery across the current local network link.
5. **Port numbers** identify the application or service receiving the traffic.

For example, a browser may connect from a temporary client port such as `54321` to destination port `443`, which is commonly used for HTTPS.

---

## 6. The Packet Journey

The request travels from the client toward the web server, and the response returns along the reverse path.

| Stage | Device / Location | Role |
|---|---|---|
| 1 | Client laptop | Encapsulation begins. The HTTPS request is created and wrapped layer by layer. |
| 2 | Access point / switch | Relays wireless or wired traffic across the local network. |
| 3 | Router | Routes the IP packet toward the internet and may perform Network Address Translation (NAT). |
| 4 | Internet | The traffic travels through multiple interconnected networks and routers. |
| 5 | Firewall | Applies security rules and controls before permitted traffic reaches the server. |
| 6 | Web server | Receives the traffic, de-encapsulates the request, processes it, and prepares a response. |

### Request Direction

**Client → Access Point/Switch → Router → Internet → Firewall → Web Server**

### Response Direction

**Web Server → Firewall → Internet → Router → Access Point/Switch → Client**

The actual internet path can contain many more routers and network devices than shown in this simplified example.

---

## 7. What Happens When the Website Is Opened?

When the user enters `https://example.com`, several processes occur before the web page is displayed.

### Step 1: DNS Resolution

The browser needs the IP address associated with `example.com`. DNS is used to translate the human-readable domain name into an IP address.

### Step 2: Establishing a TCP Connection

After obtaining the destination IP address, the client establishes a TCP connection with the web server. TCP provides reliable, ordered delivery between the endpoints.

### Step 3: TLS Security

Because the website uses **HTTPS**, TLS is used to secure the communication. TLS helps provide encryption and authentication so that data exchanged between the client and server is protected against unauthorized observation or modification.

### Step 4: HTTP Request

The browser sends an HTTP request through the established secure connection. The request asks the web server for the required resource.

### Step 5: Server Response

The web server processes the request and sends an HTTP response back to the client.

### Step 6: De-encapsulation and Display

As the response reaches the laptop, the networking layers process the data in reverse order. The browser then interprets the response and displays the web page to the user.

---

## 8. Security in the Communication

Security is an important part of opening a secure website.

### TLS Encryption

TLS protects the communication between the browser and the web server by encrypting application data. This makes it more difficult for unauthorized parties on the network to read the contents of the communication.

### Firewall

A firewall can inspect network traffic and apply security rules. It can allow legitimate traffic while blocking traffic that violates configured security policies.

### HTTPS

HTTPS is HTTP carried over a secure TLS connection. It is commonly used to protect web traffic, especially when sensitive information is being exchanged.

Together, these mechanisms help protect communication between the client and the web server.

---

## 9. Key Takeaways

The following points summarize the main concepts discussed in this report:

1. A single secure page load uses all four layers of the TCP/IP stack.
2. **Encapsulation** adds protocol information as data moves down the networking stack.
3. The PDU changes from **message → segment → packet → frame** as data moves downward.
4. The TCP/IP model has four layers, while the OSI model has seven layers.
5. The top three OSI layers—Application, Presentation, and Session—are generally represented by the TCP/IP Application layer.
6. The URL/FQDN provides a human-readable name, while DNS resolves it to an IP address.
7. IP addresses support logical addressing and routing between networks.
8. MAC addresses are used for local-link delivery.
9. Port numbers identify the application or service involved in a connection.
10. The source and destination IP addresses normally remain associated with the end-to-end communication, although NAT can change addresses at network boundaries.
11. MAC addresses are link-local and can change from one network hop to another.
12. TLS and firewalls provide important security controls along the communication path.

---

## 10. Conclusion

Opening a secure website is a good example of how multiple networking technologies work together. Although the process appears simple to the user, several protocols and networking layers operate behind the scenes.

DNS resolves the website name, TCP provides reliable transport, IP handles logical addressing and routing, MAC addresses support local-link delivery, ports identify applications, and TLS protects HTTPS communication. Routers, switches, access points, firewalls, and web servers each perform different roles as the request travels through the network.

Understanding this process provides a practical view of the TCP/IP model and shows how networking concepts work together to deliver a secure web page from a server to a user's device.

---

## 11. Source Note

This report is based on the six slides of the **TEAM-04 presentation file (`TEAM_-7.pptx`)** provided for the WADF105 course presentation.

The report expands and organizes the concepts presented in the slides into a structured written report. Additional explanatory material has been included to make the networking process clearer and more suitable for report submission.

---

## 12. Presentation Information

| Item | Details |
|---|---|
| **Course** | WADF105 |
| **Group** | TEAM-04 |
| **Programme** | FCDF-COHORT-11 |
| **Level** | Level 1, Semester 1 |
| **Presentation Date** | 30 September 2026 |
| **Presenter 1** | Isa Sani Alhassan — C11/26/FCDF17171 |
| **Presenter 2** | Lelah Naomie — C11/26/FCDF17184 |
| **Representing** | TEAM-04 |
