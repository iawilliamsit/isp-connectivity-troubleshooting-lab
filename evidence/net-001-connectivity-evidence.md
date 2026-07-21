# NET-001 Evidence Summary: ISP Connectivity and Web Timeout Issue

## Issue Observed

The network appeared connected, but normal web traffic was not completing. Devices had local connectivity, DNS was resolving, and traffic was visible in monitoring, but web requests timed out.

## Local Checks Completed

- Confirmed the Raspberry Pi had network connectivity.
- Confirmed the local router was reachable.
- Confirmed the ISP router was reachable.
- Confirmed public IP addresses were reachable.
- Confirmed DNS resolution worked through router DNS.
- Confirmed DNS resolution worked through public DNS.
- Confirmed ntopng showed active traffic flow.
- Confirmed the ISP router responded to Nmap/Zenmap scanning.
- Confirmed web requests were timing out after DNS resolution.

## Tools / Methods Used

- Raspberry Pi terminal
- ntopng traffic monitoring
- Pi-hole DNS observation
- Nmap / Zenmap router scanning
- DNS testing with nslookup
- Connectivity testing with ping
- Web traffic testing with curl
- Router reachability testing

## Evidence Collected

- Router reachability was confirmed.
- ISP router reachability was confirmed.
- DNS resolution worked through multiple DNS paths.
- ntopng showed active network traffic.
- Nmap/Zenmap confirmed the router was alive and responding locally.
- Web traffic testing showed timeout behavior.
- The issue appeared narrower than a full internet outage or DNS failure.

## Finding

The evidence suggested that the issue was not a complete local network failure and not a complete DNS failure.

The network had connectivity, DNS was resolving, and traffic was visible, but web traffic was not completing normally. The likely issue area was the ISP/router path, web/TCP traffic completion, router behavior, or IPv6/path handling.

## Escalation

The issue was prepared for ISP escalation because local testing showed that basic connectivity and DNS were working, but web traffic was still failing.

The ISP could be given specific evidence instead of a vague report that “the internet is not working.”

## Result

The troubleshooting process narrowed the issue and created escalation-ready documentation. The investigation showed that the problem was more specific than basic LAN or DNS failure.

## Sanitization Note

No public IP addresses, account numbers, router serial numbers, Wi-Fi passwords, ISP account details, customer data, or private screenshots are included.
