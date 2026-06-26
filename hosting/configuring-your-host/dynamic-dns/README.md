# Dynamic DNS

Most ISPs assign dynamic IP addresses for their residential and small business accounts. Dynamic IPs can change over time. Dynamic IPs are more cost-effective, but they present a challenge for hosts which require consistent connectivity.

In contrast, a static IP address remains fixed and does not change. It is manually assigned to a device or service, providing a stable point of contact for hosting purposes. Static IPs are typically used by large organizations, dedicated servers, or services that require constant accessibility. While static IPs offer reliable connectivity, they are generally more expensive than dynamic IPs.

Dynamic DNS (DDNS) services help hosts with dynamic IP addresses. `hostd` has built-in DDNS and integrates with multiple services, including Cloudflare, AWS Route53, DuckDNS, and No-IP. With `hostd`'s built-in DDNS, hosts can use DDNS without downloading and setting up external software.

## Benefits of DDNS

**Connectivity:** Dynamic DNS lets hosts with dynamic IP addresses stay connectable, even when their IP changes. DDNS services monitor and update the IP address associated with a domain name. When the IP changes, incoming traffic is redirected to the new IP.

**Cost:** With dynamic DNS, hosts can avoid frequent IP announcements, which cost time, effort, and Siacoin. DDNS services update IP address information automatically, so hosts don't have to manage it manually.
