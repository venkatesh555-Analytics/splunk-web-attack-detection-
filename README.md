# splunk-web-attack-detection-
Threat hunting project using Splunk (HTTP log analysis)
# Web Attack Detection using Splunk

## Objective

To detect suspicious web activity and identify potential attacks by analyzing Apache HTTP logs using Splunk SIEM.

---

## Tools & Technologies

* Splunk SIEM
* SPL (Search Processing Language)
* Apache HTTP Logs

---

## Dataset

* Apache HTTP log dataset (~10,000 events)
* Fields analyzed:

  * clientip
  * uri_path
  * status
  * useragent

---

##  Project Workflow

### 1. Data Ingestion

* Uploaded HTTP log file into Splunk
* Indexed data for search and analysis

### 2. Data Exploration

* Verified logs using:

  
  index=*
  
* Identified key fields for analysis

### 3. Detection Strategy

* Identified top client IPs
* Filtered HTTP 404 errors (suspicious behavior)
* Analyzed number of unique URLs accessed
* Investigated abnormal access patterns

---

## Key SPL Queries

### Identify Top IPs

```spl
index=* 
| stats count by clientip
| sort -count
| head 10
```

### Detect Suspicious 404 Errors

```spl
index=* status=404
| stats count by clientip
| sort -count
```

### Identify Scanning Behavior

```spl
index=* status=404
| stats dc(uri_path) as unique_urls count by clientip
| sort -unique_urls
```

### Investigate Suspicious IP Activity

```spl
index=* clientip=144.76.95.39
| table _time uri_path status
```

---

## Findings

* Suspicious IP: **144.76.95.39**
* Generated multiple HTTP 404 errors
* Accessed multiple endpoints:

  * /articles/
  * /scripts/
  * /blog/
* Accessed **10+ unique URLs**
* Behavior indicates **directory scanning / reconnaissance attack**

---

## Attack Timeline

* Initial access from IP
* Rapid requests to multiple endpoints
* Continuous 404 responses
* Pattern indicates automated scanning activity

---

## Indicators of Compromise (IOC)

* IP Address: 144.76.95.39
* Multiple failed requests (404 errors)
* Access to non-existent endpoints

---

## Dashboard Visualizations

* Top Suspicious IPs (Bar Chart)
* Status Code Distribution (Pie Chart)
* Traffic Trend Over Time (Line Chart)
* Attack Details (Table)

---

---

##  Conclusion

This project successfully detected suspicious web activity using Splunk by analyzing HTTP logs. The identified IP demonstrated behavior consistent with directory scanning, indicating reconnaissance activity targeting web resources.

---

## Recommendations

* Block suspicious IP addresses
* Implement rate limiting
* Monitor repeated 404 errors
* Deploy Web Application Firewall (WAF)

---
