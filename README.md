# ISP Connectivity Troubleshooting Lab

## Project Summary

This project documents a home network troubleshooting session where local connectivity was present, DNS resolution was working, and traffic was visible in ntopng, but web traffic was timing out.

The goal was to determine whether the problem was caused by the local network, Pi-hole DNS, router reachability, DNS resolution, web/HTTPS traffic, or the ISP/router path.

## Scenario

The network appeared connected, but internet access was not behaving normally. Devices had a connection, but web traffic did not complete as expected.

Initial symptoms included:

* Local network connection was active
* Router was reachable
* DNS resolution worked
* ntopng showed traffic flow
* Web requests timed out
* ISP router responded to scans and local tests

## Tools Used

* Raspberry Pi
* ntopng
* Pi-hole
* Nmap / Zenmap
* Linux terminal
* `ping`
* `nslookup`
* `curl`
* `traceroute`
* Router reachability testing

## Troubleshooting Goal

The goal was to answer:

* Is the Raspberry Pi connected to the local network?
* Can the Pi reach the home router?
* Can the Pi reach the ISP router?
* Can the Pi reach the internet by IP address?
* Is DNS working?
* Is web/HTTPS traffic completing?
* Is the router alive and responding to services?
* Is the issue local, DNS-related, router-related, or ISP-side?

## Commands Used

### Check local IP and route

```bash
hostname -I
ip route
cat /etc/resolv.conf
```

### Test local gateways

```bash
ping -c 5 192.168.68.1
ping -c 5 192.168.1.1
```

### Test internet by IP

```bash
ping -c 5 1.1.1.1
ping -c 5 8.8.8.8
```

### Test DNS resolution

```bash
nslookup google.com
nslookup google.com 192.168.1.1
nslookup google.com 1.1.1.1
nslookup google.com 127.0.0.1
```

### Test web traffic

```bash
curl -I --max-time 10 https://example.com
curl -4 -I --connect-timeout 5 --max-time 10 https://example.com
curl -4 -I --connect-timeout 5 --max-time 10 http://example.com
```

### Router scan

```bash
sudo nmap -Pn -n --reason -p 53,67,80,443,123,1900,5000,5060,7547,8080,8443 192.168.68.1 192.168.1.1
```

### Deeper router service review

```bash
sudo nmap -sV -Pn -n --reason -p 1-10000 192.168.1.1
```

## Key Observations

### Local router path

The Raspberry Pi was able to reach the local gateway and ISP router. This showed that the local network path was active.

### DNS

DNS resolution worked through both the ISP router and public DNS.

This meant the issue was not a complete DNS failure.

### Internet by IP

The Raspberry Pi was able to reach public IP addresses such as `1.1.1.1`.

This showed that basic internet reachability existed.

### Web traffic

Web requests using `curl` timed out.

This showed that the issue was narrower than basic connectivity or DNS. The problem appeared related to web/TCP/HTTPS traffic completion, router behavior, ISP routing, or IPv6/path behavior.

### ntopng

ntopng showed active traffic between local hosts, Pi-hole, router addresses, and external destinations.

This confirmed that traffic was present and visible, even while web access was not completing normally.

### Nmap / Zenmap

Nmap confirmed the ISP router was alive and responding locally on several services.

Router response did not prove internet service was fully working, but it helped confirm that the device was reachable and active on the local path.

## Finding

The issue did not appear to be:

* A complete LAN outage
* A complete DNS failure
* A Raspberry Pi service failure
* A total router reachability failure

The evidence suggested a narrower issue involving web traffic completion, router behavior, ISP-side service handling, or the upstream internet path.

## Business / Support Value

This project demonstrates a layered troubleshooting process:

1. Confirm local device connectivity
2. Confirm gateway reachability
3. Confirm ISP router reachability
4. Test internet by IP
5. Test DNS separately
6. Test web traffic separately
7. Use monitoring to observe actual traffic
8. Use scanning to confirm router response
9. Document findings for escalation

This type of troubleshooting helps reduce wasted time because it separates “connected” from “working.”

## Skills Demonstrated

* Network troubleshooting
* DNS testing
* Router reachability testing
* Nmap scanning
* ntopng traffic observation
* Linux command-line testing
* Web traffic testing with `curl`
* Evidence-based documentation
* ISP escalation preparation
* Technical note writing

## Sanitization Note

No public IP addresses, private account details, router serial numbers, Wi-Fi passwords, customer data, or ISP account information are included in this repository.
