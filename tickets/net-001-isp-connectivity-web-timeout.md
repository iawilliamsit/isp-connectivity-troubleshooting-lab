# NET-001: ISP Connectivity Issue With Web Traffic Timeout

## Platform Style

Jira Service Management / ServiceNow Incident

## Ticket Fields

* Ticket ID: NET-001
* Type: Incident
* Request Type: Network / Internet Connectivity Issue
* Status: Resolved / Escalated to ISP
* Priority: High
* Impact: Internet connection was present, but normal web traffic was not completing
* Urgency: Same-day troubleshooting needed
* Category: Network Connectivity
* Subcategory: ISP / Router / Web Traffic
* Service: Home Internet / LAN Connectivity
* Assigned Group: Network Support
* Assigned To: Isaiah Williams

## Issue Report

Internet service appeared connected, but web traffic was timing out. Devices had local connectivity, DNS was responding, and network traffic was visible, but normal browsing behavior was not completing as expected.

## Business / User Impact

The network could not be trusted for normal internet use even though it appeared connected. This created a confusing issue where basic network checks passed, but web access still failed.

## Initial Observations

* Local network connection was active.
* The router was reachable.
* DNS resolution worked through both router DNS and public DNS.
* ntopng showed active traffic on the network.
* Nmap/Zenmap showed the ISP router was alive and responding locally.
* Web traffic testing showed timeout behavior.
* The issue did not look like a complete LAN outage or complete DNS failure.

## Questions Asked

* Can the device reach the local router?
* Can the device reach the ISP router?
* Can the device reach a public IP address?
* Is DNS resolving names correctly?
* Is web traffic completing after DNS resolution?
* Is the issue affecting one device or multiple devices?
* Is the router responding locally?
* Does monitoring show traffic moving through the network?

## Troubleshooting Steps

1. Confirmed the Raspberry Pi had local network connectivity.
2. Confirmed the local router was reachable.
3. Confirmed the ISP router was reachable.
4. Tested public IP reachability using ping.
5. Tested DNS resolution through the router.
6. Tested DNS resolution through public DNS.
7. Used ntopng to confirm traffic visibility.
8. Used Nmap/Zenmap to verify the router was alive and responding on local services.
9. Tested web traffic using curl.
10. Confirmed that DNS worked, but web requests timed out.
11. Narrowed the issue away from basic LAN connectivity and DNS.
12. Identified the likely issue area as router behavior, ISP path, web/TCP traffic completion, or IPv6/path handling.
13. Prepared findings for ISP escalation.

## Tools Used

* Raspberry Pi
* ntopng
* Pi-hole
* Nmap / Zenmap
* Linux terminal
* ping
* nslookup
* curl
* traceroute
* Router admin/reachability checks

## Evidence Collected

* Router was reachable from the local network.
* ISP router responded to local scans.
* DNS resolution worked through router DNS and public DNS.
* ntopng showed traffic moving across the network.
* Public IP reachability was present.
* Web requests timed out after DNS resolution.
* The issue was narrower than a total internet outage.

## Finding

The issue did not appear to be caused by a complete local network failure or DNS failure. Evidence showed that the network was connected, DNS was resolving, and traffic was visible, but web traffic was not completing normally.

The most likely issue area was the ISP/router path, web/TCP traffic completion, router behavior, or IPv6/path handling.

## Customer / ISP Communication

Explained that local testing had already confirmed router reachability, DNS resolution, and traffic visibility. The issue was described as web traffic timing out after basic connectivity and DNS tests passed.

## Internal Work Notes

This troubleshooting process helped separate connection status from service functionality. The network appeared connected, but the evidence showed that not all traffic was completing successfully.

The issue was documented using layered troubleshooting instead of guessing or only rebooting equipment.

## Resolution

Resolved or escalated after ISP-side review and correction.

## Resolution Code

Resolved by ISP / Network Path Correction

## Escalation Needed?

Yes

## Escalation Details

Escalated to ISP because local testing showed DNS and local connectivity were working, but web traffic was still timing out. Evidence suggested the problem was beyond basic local device troubleshooting.

## Knowledge Base Opportunity

Create a network troubleshooting guide covering:

* Local gateway reachability
* ISP router reachability
* Public IP testing
* DNS testing
* Web traffic testing
* ntopng traffic review
* Nmap router checks
* IPv4 versus IPv6 testing
* When to escalate to ISP

## What This Ticket Demonstrates

* Layered network troubleshooting
* DNS testing
* Router reachability testing
* ntopng traffic observation
* Nmap scanning
* Linux command-line troubleshooting
* Evidence-based escalation
* Technical documentation
* Understanding that connected does not always mean working
