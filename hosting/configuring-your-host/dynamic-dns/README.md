---
description: Learn about the benefits of DDNS for hosts with dynamic IP addresses
---

# Dynamic DNS

Most ISPs assign dynamic IP addresses for their residential and small business accounts. Dynamic IPs can change over time. Dynamic IPs are more cost-effective, but they present a challenge for hosts which require consistent connectivity.

In contrast, a static IP address remains fixed and does not change. It is manually assigned to a device or service, providing a stable point of contact for hosting purposes. Static IPs are typically used by large organizations, dedicated servers, or services that require constant accessibility. While static IPs offer reliable connectivity, they are generally more expensive than dynamic IPs.

Dynamic DNS (DDNS) services offer a practical solution for hosts with dynamic IP addresses. `hostd` Has built-in DDNS and integrates with multiple services, including Cloudflare, AWS Route53, DuckDNS, and No-IP. By using `hostd`Its built-in DDNS hosts get the benefits of DDNS without needing to download and set up external software.

## Benefits of DDNS

**Seamless Connectivity:** Dynamic DNS enables hosts with dynamic IP addresses to stay easily connectable, even when their IP changes. DDNS services monitor and update the IP address associated with a domain name in real-time. This automated process redirects incoming traffic to the new IP, ensuring consistent accessibility for hosted services.

**Cost-Efficiency:** With dynamic DNS, hosts can avoid the need for frequent IP announcements, which can incur costs in terms of time, effort, and even Siacoin. Active DNS services provide a reliable and automated updating of IP address information. This cost-effective approach allows hosts to focus on delivering their services rather than managing IP logistics.
