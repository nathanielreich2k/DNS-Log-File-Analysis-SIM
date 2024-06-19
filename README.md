# DNS Log File Analysis using Splunk SIEM

## Introduction
✨DNS (Domain Name System) logs play a vital role in comprehending network operations and pinpointing possible security risks. Splunk SIEM (Security Information and Event Management) offers robust features to analyze DNS logs effectively, enabling the detection of irregularities and potential malicious behaviors.

## Skills Learned
-Interacting with the Splunk platform to search for our log files. Including DNS, HTTP, and SSH events.

-Extraction of key information such as IP addresses, login attempts, query type, and response code.

-Observation of anomalies within the data and the impact they could have on an organization.

-Researching and detecting malicious DNS domains to understand what could be causing impact.


## Steps

✨ LAB NAME: DNS Log File Analysis using Splunk SIEM

✨ OBJECTIVE: The aim is to capture and observe log data within Splunk for anomalies and potential malicious activity.

✨ THEORY: Multiple online log files will be uploaded into Splunk to observe the data shown.


### 1. Prepare Sample DNS Log Files for upload to Splunk
- Obtained a free sample online of a DNS log file. 
- Saved the sample log files in a directory accessible by the Splunk instance.

*Ref 1: 
```
index=* sourcetype=dns_sample
```

### 2. Extract Relevant Fields
-Locate important categories within DNS logs such as originating IP address, target IP address, domain name, request type, response status code, and others.

-As illustrated here:" | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b": " This regular expression is designed to identify typical DNS-related terms within the unprocessed event data.

-Sample command for extraction:
```
index=* sourcetype=dns_sample | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```

### 3. Identify irregularities in the data
- Observing for unusual anomalies or changes in the data for DNS queries.
- Example query to identify surges.
```
index=_* OR index=* sourcetype=dns_sample  | stats count by fqdn
```

### 4. Find the top DNS sources
- Use the top command to count each query type and the occurrences:   
```
index=* sourcetype=dns_sample | top fqdn, src_ip
```








































