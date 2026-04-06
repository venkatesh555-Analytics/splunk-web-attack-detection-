# Project Documentation: Web Attack Detection using Splunk

---

## Objective

The objective of this project is to detect suspicious web activity and identify potential attacks by analyzing Apache HTTP logs using Splunk SIEM.

---

## Tools & Technologies

* Splunk SIEM
* SPL (Search Processing Language)
* Apache HTTP Logs

---

## Dataset Details

* Source: Apache HTTP log dataset
* Size: ~10,000 events
* Fields analyzed:

  * clientip
  * uri_path
  * status
  * useragent

---

##  Project Workflow

### 1. Data Ingestion

* Uploaded HTTP log file into Splunk
* Indexed data for searching and analysis

---

### 2. Data Exploration

* Verified log data using:


  index=*
 
* Identified available fields (clientip, uri_path, status)

---

### 3. Detection Strategy

#### a) Identify Top IPs

* Used aggregation to find high-traffic IPs

#### b) Filter Suspicious Activity

* Focused on HTTP status **404 errors**
* Indicates attempts to access non-existent resources

#### c) Detect Scanning Behavior

* Calculated number of unique URLs accessed per IP
* High number of unique URLs indicates scanning

---

### 4. Investigation

* Identified suspicious IP: **144.76.95.39**
* Observed behavior:

  * Multiple 404 errors
  * Access to different endpoints:

    * /articles/
    * /scripts/
    * /blog/

---

### 5. Attack Analysis

The IP demonstrated:

* High number of failed requests
* Access to multiple unique paths
* Non-human browsing pattern

This indicates:
**Directory Scanning / Web Reconnaissance Attack**

---

## Timeline of Activity

* Initial request from IP
* Rapid access to multiple endpoints
* Continuous 404 responses

---

## Indicators of Compromise (IOC)

* Suspicious IP: 144.76.95.39
* Multiple invalid URL requests
* High volume of HTTP 404 responses

---

## Visualization

* Created Splunk dashboards including:

  * Top IPs (Bar Chart)
  * Status Code Distribution (Pie Chart)
  * Traffic Trends (Line Chart)
  * Attack Details (Table)

---

## Conclusion

The project successfully identified suspicious web activity using log analysis techniques. The behavior of the detected IP strongly indicates reconnaissance activity aimed at discovering hidden web resources.

---

## Recommendations

* Block suspicious IP addresses
* Implement rate limiting
* Monitor repeated 404 requests
* Use Web Application Firewall (WAF)

---
