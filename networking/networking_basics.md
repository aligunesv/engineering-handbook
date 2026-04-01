# NETWORKING NOTES

## 1. Basics

Early systems were very simple:
- Only one server existed
- All applications ran on that server

Main problem:
- How do users reach this server?

---

## 2. IP Address

Every device on a network has an address called an IP address.

- Acts as the identity of the device on the network
- Unique within the network

Analogy:
- IP = building address

Example:
- 192.168.1.1

---

## 3. DNS (Domain Name System)

IP addresses are hard to remember. DNS solves this problem.

Purpose:
- Converts domain names to IP addresses

Example:
- google.com → IP address

Summary:
- DNS = name-to-address translation system

---

## 4. Ports

As servers started running multiple services:
- Website
- Database
- Payment system

They needed a way to differentiate services on the same IP.

Solution: Port

- Each service uses a different port
- Acts like different doors in the same building

Examples:
- 80 / 443 → Web (HTTP / HTTPS)
- 3306 → MySQL

Analogy:
- IP = building
- Port = apartment number

---

## 5. Subnet (Subnetting)

As the system grows, organization and security become important.

Subnet:
- Dividing a network into smaller parts

Example:
- Frontend subnet
- Backend subnet
- Database subnet

Purpose:
- Better organization
- Security isolation

Analogy:
- Different floors in the same building

---

## 6. Routing

How do different subnets or networks communicate?

Routing:
- Determines the path data takes
- Helps find the correct route in the network

Analogy:
- Works like GPS

---

## 7. Firewall

One of the most critical parts of network security.

Firewall:
- Controls who can access which service

Example rules:
- Only ports 80 and 443 are open to the internet
- Database is accessible only by the backend

Analogy:
- Security gate

---

## 8. NAT (Network Address Translation)

Many servers are not directly exposed to the internet.

Situation:
- Backend servers use private IPs
- They still need internet access

NAT:
- Allows private IPs to use a single public IP for outgoing traffic

Purpose:
- IP conservation
- Security

Analogy:
- Shared company phone line

---

## 9. Cloud Systems

Instead of physical servers, cloud systems are used.

Key concepts remain the same:
- VPC (Virtual Private Cloud)
- Subnets
- Routing
- Firewall
- NAT

Advantages:
- Easier management
- Flexible
- Scalable

---

## 10. Docker (Containers)

Classic problem:
- “It works on my computer” issue

Docker solution:
- Packages the application and its dependencies together
- Ensures consistent behavior across environments

Analogy:
- Portable application box

---

## 11. Kubernetes

When the number of containers grows, management becomes hard.

Kubernetes:
- Automatically manages containers
- Scales applications
- Fixes failures automatically

Key concepts:
- Pod → Group of one or more containers
- Service → Stable access point
- Ingress → Routes external traffic

---

## SUMMARY

| Concept  | Meaning                           |
|----------|----------------------------------|
| IP       | Device address                    |
| DNS      | Name → IP translation             |
| Port     | Service door                      |
| Subnet   | Dividing the network              |
| Routing  | Path determination                |
| Firewall | Access control                    |
| NAT      | Access to external network        |
