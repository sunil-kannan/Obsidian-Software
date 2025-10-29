---
date: "2025-10-26"
tags: 
link:
---

# Service Level Agreement (SLA) 

**SLA (Service Level Agreement)** is a formal contract or commitment that defines the **expected level of service** between a service provider and a customer.

It outlines measurable performance targets and remedies if those targets aren’t met.

---

## 🔧 Common SLA Metrics
| Metric | Description | Example |
|---------|--------------|----------|
| **Uptime / Availability** | % of time the service is operational | 99.9% uptime |
| **Response Time** | How quickly support responds to an issue | Within 1 hour |
| **Resolution Time** | How fast an issue must be fixed | Within 4 hours |
| **Performance** | Throughput, latency, or speed guarantees | < 200 ms latency |

---

## 📉 Low SLA — Why Some Choose It
Not every service needs “five nines” reliability.

**Reasons for choosing a lower SLA:**
1. 💰 **Cost savings** — Higher SLAs require redundancy and support, which are expensive.  
2. ⚙️ **Fit for purpose** — Internal or non-critical apps can tolerate downtime.  
3. 🧠 **Simpler operations** — Less need for 24/7 monitoring.  
4. 📊 **Balanced trade-off** — Cheaper, simpler, and good enough for certain workloads.

---

## ⚖️ SLA Violations and Penalties

### 1. **Service Credits (most common)**
- Customer receives **bill credits** for downtime or performance shortfalls.
- Example:  
  - SLA: 99.9% uptime  
  - Actual: 99.0%  
  - → 10% service credit on next bill.

### 2. **Financial Penalties**
- In enterprise or government contracts, direct financial compensation may apply.
- Example: $500 per hour of downtime.

### 3. **Termination Rights**
- Repeated SLA breaches may allow the customer to **terminate the contract**.

### 4. **Reputational Consequences**
- Providers risk trust and contract renewals when they fail SLAs.

---

## 🏢 Example — AWS DynamoDB SLA

- **AWS DynamoDB SLA:** 99.99% Monthly Uptime Percentage.  
- **If breached:** Customer may request **Service Credits** (not refunds).  
- **Exclusions:**  
  - Customer-side issues  
  - Force majeure  
  - Factors outside AWS’s reasonable control  

### 💡 AWS Outage Case (Oct 2025)
- Recent **DynamoDB DNS issue** in `us-east-1` caused major disruption.  
- Customers may be **eligible for credits** if uptime fell below 99.99% and if they submit an SLA claim.  
- Credits are **limited** and applied to future bills, **not cash refunds**.

---

## 📊 SLA Levels and Downtime

| SLA (%) | Max Downtime per Month | Max Downtime per Year |
|----------|------------------------|------------------------|
| 99% | ~7.3 hours | ~3.65 days |
| 99.9% | ~43.8 minutes | ~8.76 hours |
| 99.99% | ~4.4 minutes | ~52.6 minutes |
| 99.999% | ~26 seconds | ~5.26 minutes |

---

## 🧾 Key Takeaways
- SLA defines the **service quality guarantee** and **recourse** for failure.  
- **Low SLA** = cheaper, simpler, but more downtime risk.  
- **Penalties** are usually **service credits**, not large payouts.  
- Always **read the exclusions** and **submit claims** within deadlines.


![[SLA.png]]

![[KPI (Key Performance Indicator).png]]

![[KPI vs SLA.png]]