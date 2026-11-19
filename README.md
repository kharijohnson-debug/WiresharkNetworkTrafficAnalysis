# WiresharkNetworkTrafficAnalysis
Conducted SOC-focused network traffic analysis using Wireshark, examining DNS resolution, query patterns, and potential security anomalies through packet inspection and traffic visualization.

Wireshark Network Traffic Analysis

Project Overview

This project documents a hands-on network traffic investigation conducted using Wireshark on macOS. The objective was to capture live network traffic, analyze Domain Name System (DNS) activity, examine packet-level communication, and identify potential indicators of suspicious network behavior.

The investigation applied foundational Security Operations Center (SOC) analysis techniques, including packet inspection, DNS transaction correlation, protocol filtering, traffic visualization, and evidence-based reporting.

Tools and Technologies

Wireshark: Packet capture, protocol analysis, and traffic visualization

macOS: Host operating system

DNS: Domain name resolution and query-response analysis

Wireshark Display Filters: Targeted inspection of network activity

Wireshark Statistics and I/O Graphs: Traffic measurement and visualization

Investigation Objectives

Capture and inspect live network traffic.

Identify DNS queries and corresponding responses.

Examine DNS transaction identifiers, response codes, and resolution behavior.

Investigate unusually long domain names as potential indicators requiring further analysis.

Analyze DNS traffic volume and query-response patterns.

Document findings and determine whether the observed traffic provides evidence of malicious activity.

Methodology

1. Network Traffic Capture

Captured approximately 25,086 packets using Wireshark on the Mac's Wi-Fi interface (en0).

Applied the dns display filter to isolate DNS traffic from the broader network capture.

2. DNS Query and Response Inspection

Inspected DNS packets to understand how the host requested domain name resolution and received responses.

Analyzed:

DNS transaction identifiers

Requested domain names

Query and response flags

Resolved IPv4 addresses

DNS response times

Time-to-live (TTL) values

One examined transaction involved the domain clients1.google.com, which resolved to 142.251.211.174, with an observed response time of approximately 119.616 milliseconds.

3. DNS Anomaly Investigation

Applied targeted Wireshark display filters to investigate DNS behavior.

Display Filter

Investigation Purpose

dns

Isolate DNS traffic

dns.flags.response == 0

Identify DNS queries

dns.flags.response == 1

Identify DNS responses

dns.flags.rcode == 3

Identify NXDOMAIN responses

dns.qry.name.len > 50

Identify longer DNS query names

dns.flags.response == 0 && dns.qry.name.len > 50

Isolate long-domain DNS queries

The investigation identified several long DNS query names associated with common cloud and web services.

Long domain names can warrant further investigation, but their length alone does not establish malicious activity or DNS tunneling.

4. DNS Statistical Analysis

Used Wireshark's DNS statistics to examine the captured traffic.

Metric

Observed Result

DNS packets

620

DNS queries

310

DNS responses

310

DNS retransmissions

0

Unsolicited DNS responses

0

DNS error responses

0

Average response time

22.98 ms

The observed query and response counts were balanced, with no DNS error responses reported in the analyzed sample.

5. DNS Traffic Visualization

Configured Wireshark I/O Graphs to visualize DNS traffic over time.

Created separate plots for:

DNS Queries: dns.flags.response == 0

DNS Responses: dns.flags.response == 1

Used a one-second interval to compare packet rates and identify traffic fluctuations.

The graph showed similar query and response activity patterns, with peak DNS traffic approaching approximately 50 packets per second.

Security Findings

Finding 1 — DNS Resolution Behavior

The captured sample contained 310 DNS queries and 310 responses, with no reported DNS error responses or retransmissions.

Finding 2 — Long Domain Names

Several DNS queries contained domain names exceeding 50 characters. These were investigated as potential anomalies, but the observed names did not independently establish malicious behavior.

Finding 3 — DNS Traffic Patterns

DNS traffic volume fluctuated throughout the capture. Query and response activity generally followed similar patterns, without a clearly established malicious traffic pattern.

Finding 4 — Investigation Limitations

The capture represented a short observation period. The absence of identified malicious DNS behavior does not establish that the network was free of threats.

Conclusion

This investigation demonstrated practical experience with network packet analysis, DNS protocol inspection, anomaly investigation, and traffic visualization using Wireshark.

No conclusive evidence of malicious DNS activity was identified within the analyzed capture.

The project strengthened foundational SOC Analyst skills in:

Network traffic monitoring

Protocol analysis

DNS investigation

Security anomaly triage

Evidence-based technical reporting

Distinguishing potential indicators from confirmed threats

Future Improvements

Analyze longer network captures to establish baseline DNS behavior.

Compare normal DNS traffic against authorized simulated suspicious activity.

Investigate DNS tunneling indicators in a controlled laboratory environment.

Expand analysis to HTTP, TLS, and TCP traffic.

Document additional investigations using packet captures and supporting evidence.
