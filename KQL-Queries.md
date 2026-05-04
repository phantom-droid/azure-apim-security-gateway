# 📊 KQL Queries — API Rate Limiting & Security Gateway

> Queries used in this project via **Application Insights → Logs**.
> Resource: `apim-logging-insights` | Workspace: Log Analytics (Default)

---

### 1. All API Requests (Latest First)
> Core query used in the project to verify that Application Insights is capturing all APIM requests.
```kql
requests
| order by timestamp desc
| take 20
```

---

### 2. Failed Requests Only (4xx / 5xx)
> Filter to see only requests that failed — useful to spot auth failures and errors.
```kql
requests
| where success == false
| project timestamp, name, resultCode, duration, url, client_IP
| order by timestamp desc
| take 20
```

---

### 3. Rate Limited Requests — 429 Too Many Requests
> Shows requests blocked by the `rate-limit-by-key` policy (10 calls / 60 sec).
```kql
requests
| where resultCode == "429"
| project timestamp, url, client_IP, duration
| order by timestamp desc
```

---

### 4. Unauthorized Requests — 401 Access Denied
> Shows requests rejected due to a missing or wrong `Ocp-Apim-Subscription-Key`.
```kql
requests
| where resultCode == "401"
| project timestamp, url, client_IP
| order by timestamp desc
```

---

### 5. Request Count by HTTP Status Code
> Summary of all response codes returned by the gateway — see 200, 401, 429 at a glance.
```kql
requests
| where timestamp > ago(24h)
| summarize Count=count() by resultCode
| order by Count desc
```

---

### 6. Requests by Client IP
> Shows which IPs are hitting the gateway — useful to verify the IP filter policy is working.
```kql
requests
| where timestamp > ago(24h)
| summarize RequestCount=count() by client_IP
| order by RequestCount desc
```

---

## 📝 Quick Reference

| Term | Meaning |
|---|---|
| `requests` | Built-in Application Insights table — logs every API request |
| `resultCode` | HTTP status code returned (200, 401, 429, 403, etc.) |
| `success` | Boolean — false for 4xx and 5xx responses |
| `client_IP` | IP address of the caller |
| `duration` | Response time in milliseconds |
| `ago(24h)` | Filter to last 24 hours |
| `summarize` | Group and aggregate (like SQL GROUP BY) |
| `project` | Select specific columns (like SQL SELECT) |
| `order by` | Sort results |
| `take` | Limit number of rows returned |

---

*Author: Yashraj | Cloud Security Engineering Track | Azure for Students*
