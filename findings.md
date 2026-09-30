# Network Traffic Analysis Findings

## Finding 1: Network Interface and Addressing

I used `ip addr show eth0` to inspect the active network interface.

The `eth0` interface was UP and had the IPv4 address `100.115.92.195/28`. A `/28` prefix provides 16 total IPv4 addresses in the subnet.

The interface also had a link-local IPv6 address beginning with `fe80::`.

**Security takeaway:** Identifying network interfaces and their assigned addresses helps an analyst understand how a host is connected to a network and provides context for further investigation.

## Finding 2: Routing and Default Gateway

I used `ip route` to inspect the routing table.

The system used `100.115.92.193` as its default gateway through the `eth0` interface. The directly connected IPv4 subnet was `100.115.92.192/28`.

I learned that a default gateway provides a path for traffic destined for networks outside the local subnet, including traffic traveling toward other networks or the internet.

**Security takeaway:** Reviewing routing information helps an analyst understand where network traffic is expected to travel.

## Finding 3: Gateway Connectivity

I used `ping -c 4 100.115.92.193` to test connectivity to the default gateway.

All four ICMP echo requests received responses, demonstrating connectivity between the Linux environment and its gateway during the test.

**Security takeaway:** Connectivity tests can help determine whether a host can reach another network device, but successful ping responses alone do not prove that every network service is available.

## Finding 4: Active Connection Inspection

I used `ss -tun` and `ss -tn` to inspect active TCP and UDP connections.

No active connections were displayed during the initial snapshots. I then generated HTTPS traffic using `curl https://example.com`. The request successfully returned webpage content, but the TCP connection completed before it appeared in the subsequent `ss` snapshot.

**Security takeaway:** A point-in-time socket inspection can miss short-lived connections. Analysts should consider timing and use appropriate monitoring or packet-capture tools when investigating transient network activity.

## Finding 5: DNS Resolution

I used `getent hosts example.com` and `getent ahostsv4 example.com` to examine hostname resolution.

The system successfully resolved `example.com` to IPv6 and IPv4 addresses. The IPv4 lookup returned `172.66.147.243` and `104.20.23.154` during the test.

I also observed `STREAM`, `DGRAM`, and `RAW` socket-type entries in the `getent` output. These entries describe socket types and do not represent separate observed network connections.

**Security takeaway:** DNS and hostname resolution information can help analysts correlate domain names with network addresses during an investigation.
