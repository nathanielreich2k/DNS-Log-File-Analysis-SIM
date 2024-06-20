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


### 1. Prepare Sample DNS Log Files for upload to Splunk
- Obtained a free sample online of a DNS log file. [DNS log file](https://www.secrepo.com/maccdc2012/dns.log.gz)
- Saved the sample log files in a directory accessible by the Splunk instance.

*Ref 1: A simple index command was used to list all the contents of the log file.
```
index=* sourcetype="dns"  
```

### 2. Extract New Fields
-Using the new fields option on our dashboard we can create custom search options.

-These include categorizations such as originating IP address, target IP address, domain name, request type, response status code, and others.

*Ref 1: 
A sample log file was chosen that included a source IP of 198.162.21.25 and a destination of 192.168.202.136 137
![splunk 1](https://github.com/nathanielreich2k/DNS-Log-File-Analysis-SIM/assets/155709615/3121eb6f-1ec7-4196-8e17-41afa064f658)



-For more specific search queries we can use this expression which includes parsing through our data with keywords. Such as the domain, query type, and port.
-As illustrated here:" | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b": " 

This regular expression is designed to identify typical DNS-related terms within the unprocessed event data.

-Sample command for extraction:
```
index=* sourcetype=dns | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```
![splunk 2](https://github.com/nathanielreich2k/DNS-Log-File-Analysis-SIM/assets/155709615/5221818e-53c4-47da-98d0-b92ef9a84e41)

### 3. Identify irregularities in the data
- Observing for unusual anomalies or changes in the data for DNS queries.
- Example for the below query could be used to group data in a table to identify surges.
```
index=_* OR index=* sourcetype=dns  | table fqdn, src_ip, dst_ip
```
![splunk 3](https://github.com/nathanielreich2k/DNS-Log-File-Analysis-SIM/assets/155709615/e408ee37-4f23-4005-b975-2e4642b8db72)

### 4. Find the top DNS sources
- This command can be used to find the top information of each query type and the occurrences:   
```
index=* sourcetype=dns | top fqdn, src_ip
```

## Conclusion
-The above represents some commands to search and parse information to assist in finding anomalies.
-To use of short keys would be of use in this scenario for quick deployment.







































