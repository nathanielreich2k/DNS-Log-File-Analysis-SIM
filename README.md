# DNS-HTTP-SSH Log File Analysis using Splunk SIEM

## Introduction
✨DNS (Domain Name System) logs play a vital role in comprehending network operations and pinpointing possible security risks. Splunk SIEM (Security Information and Event Management) offers robust features to analyze DNS logs effectively, enabling the detection of irregularities and potential malicious behaviors.

## Skills Learned
-Interacting with the Splunk platform to search for our log files. Including DNS, HTTP, and SSH events.
-Extraction of key information such as IP addresses, login attempts, query type, and response code.
-Observation of anomalies within the data and the impact they could have on an organization.
-Researching and detecting malicious DNS domains to understand what could be causing impact.


## Steps

✨ LAB NAME: DNS-HTTP-SSH Log File Analysis using Splunk SIEM

✨ OBJECTIVE: The aim is to capture and observe log data within Splunk for anomalies and potential malicious activity.

✨ THEORY: Multiple online log files will be uploaded into Splunk to observe the data shown.


### 1. Prepare Sample DNS Log Files for upload to Splunk
- Obtained a free sample online of a DNS log file. [DNS log file](https://www.secrepo.com/maccdc2012/dns.log.gz)
- Saved the sample log files in a directory accessible by the Splunk instance.

```
index=* sourcetype=dns_sample
```

### 2. Extract Relevant Fields
- Identify key fields in DNS logs such as source IP, destination IP, domain name, query type, response code, etc.   
- As mentioned below,  | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b": This regex searches for common DNS-related keywords in the raw event data.
- Example extraction command:
```
index=* sourcetype=dns_sample | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```

### 3. Identify Anomalies
- Look for unusual patterns or anomalies in DNS activity.
- Example query to identify spikes
```
index=_* OR index=* sourcetype=dns_sample  | stats count by fqdn
```

### 4. Find the top DNS sources
- Use the top command to count the occurrences of each query type:   
```
index=* sourcetype=dns_sample | top fqdn, src_ip
```









































