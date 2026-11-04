# Simple-Network-Test-Connectivity-using-Wireshark

```markdown
# Simple Network Traffic Analysis Lab with Wireshark

## Overview
This lab demonstrates basic network connectivity testing, packet capture, and identification of common security issues using Wireshark on Parrot OS. It is a practical exercise for anyone moving from application security into broader cybersecurity engineering.

The goal is to clearly see the difference between unencrypted and encrypted traffic and understand why basic protocol choices matter.

<img width="1366" height="702" alt="CONNECT1" src="https://github.com/user-attachments/assets/0d7373b8-345e-4902-a42d-4ceecf096a14" />



## Lab Setup
- Operating System: Parrot OS
- Tools: Wireshark, Python 3, curl, ping
- Environment: Localhost / simple local services

## Steps Performed

### 1. Started a Clear-Text Service
```bash
python3 -m http.server 8080
```

### 2. Generated Traffic
```bash
ping -c 4 127.0.0.1
curl http://127.0.0.1:8080
```

### 3. Captured Traffic
- Opened Wireshark
- Selected the appropriate interface
- Started capture while generating traffic
- Stopped capture and applied filters

<img width="1364" height="703" alt="CONNECT3" src="https://github.com/user-attachments/assets/238dd1b7-72a6-4923-b6f3-8bf340d38b09" />

<img width="1366" height="726" alt="CONNECT2" src="https://github.com/user-attachments/assets/a1f10d80-45a9-438c-809d-f1e858172d9a" />

## Observations

### HTTP Traffic (`http` filter)
The full HTTP request and response were visible in clear text.  
Headers, method (GET), and response body could be read directly from the capture.  
**Security issue**: No encryption — anyone on the same network can read the data.

### ICMP Traffic (`icmp` filter)
Echo requests and replies were clearly visible.  
**Security observation**: Host discovery is possible; the system responds to ping.

### DNS Traffic (`dns` filter)
DNS queries and responses were captured, showing which domains the system was resolving.

### TLS Traffic (`tls` filter)
Handshake and encrypted application data were visible, but the actual content was unreadable.  
**Security strength**: Proper encryption protects the payload.
<img width="1365" height="730" alt="CONNECT4" src="https://github.com/user-attachments/assets/08587e67-2796-4f15-b5e4-6324eddd64b6" />

## Key Security Takeaways
- Clear-text protocols (HTTP) expose sensitive information.
- Encrypted protocols (TLS) protect data in transit.
- Simple packet captures make these differences obvious and concrete.
- Basic network visibility is an important skill when expanding from AppSec into full cybersecurity engineering.

## Recommendations
- Avoid running production or sensitive services over plain HTTP.
- Prefer HTTPS/TLS for all web traffic.
- Restrict unnecessary ICMP if host discovery is a concern.
- Regularly capture and review traffic on systems you manage to spot clear-text services.

## Tools Used
- Wireshark
- Python HTTP server
- curl
- ping

---

This lab reinforces a core principle: many security issues are still basic. Seeing clear-text versus encrypted traffic side by side is one of the fastest ways to understand why encryption and proper protocol choices matter.
```
