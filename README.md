# Network Traffic Analysis

## Project Objective

The objective of this project is to analyze basic network activity in a Linux environment and practice identifying network interfaces, listening ports, running network processes, active connections, and routing information.

## Skills Practiced

- Network interface analysis
- TCP/UDP socket inspection
- Process and port identification
- Network connectivity testing
- Routing table analysis
- Basic security investigation

## Tools and Commands Used

- `ip addr`
- `ss -tuln`
- `sudo ss -tulpn`
- `ss -tun`
- `ping`
- `ip route`

## Initial Findings

The Linux environment had an active `eth0` network interface.

UDP port 68 was listening on the system. Further investigation with `sudo ss -tulpn` identified the `dhclient` process as the process using the port.

A connectivity test using `ping` successfully sent and received four ICMP packets with 0% packet loss.

The routing table showed that network traffic used the `eth0` interface and a default gateway.

## What I Learned

This project helped me understand the difference between listening services and active network connections. I also practiced verifying which process was associated with a listening port instead of assuming a service based only on its port number.

## Disclaimer

This project was performed in my own Linux environment for educational and defensive cybersecurity purposes.
