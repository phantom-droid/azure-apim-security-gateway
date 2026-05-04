# 🔐 API Rate Limiting & Security Gateway
### Azure API Management | Cloud Security Project

> Protect APIs using native Azure cloud security mechanisms — no custom code, entirely configured through the Azure Portal UI.

---

## 📋 Project Overview

| Feature | Azure Service | Test Result |
|---|---|---|
| API Gateway | Azure API Management | ✅ 200 OK |
| Token Auth | Subscription Keys | ✅ 401 on wrong key |
| Rate Limiting | rate-limit-by-key policy | ✅ 429 after 10 reqs |
| Request Logging | Application Insights | ✅ Logs queryable |
| IP Filtering | Inbound policy | ✅ 403 on blocked IP |

---

## 🛠️ What I Built

- **API Gateway** — all traffic intercepted & security-checked before reaching the backend
- **Token Authentication** — subscription key enforcement via `Ocp-Apim-Subscription-Key` header
- **Rate Limiting** — 10 requests per 60 seconds per key, returns `retry-after` header on block
- **IP Filtering** — blocks requests from unlisted IP ranges with 403 Forbidden
- **Request Logging** — Application Insights capturing URL, status, latency, and IP in real time

---

## 📁 Files in this Repo

| File | Description |
|---|---|
| `apim.pdf` | Full step-by-step project documentation with screenshots |
| `KQL-Queries.md` | All KQL queries used in Application Insights |

---

## 🧰 Tech Stack

- Microsoft Azure (Azure for Students)
- Azure API Management (APIM) — Developer Tier
- Application Insights
- KQL (Kusto Query Language)
- httpbin.org (mock backend)

---

## 👤 Author

**Yashraj** | 1st Year Computer Engineering Student
Aspiring Cloud Security Engineer 🚀
[LinkedIn](https://bit.ly/YashrajKulkarni)
