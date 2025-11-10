---
date: "2025-11-09"
tags: 
link:
---

# 🧭 Multi-Tenant SaaS Database Architecture (Zoho CRM Style)

```mermaid
flowchart TD

    subgraph Client["🌐 Customer Request"]
        A1[User Request<br/>tenant_id = 15422]
    end

    subgraph Gateway["🚪 API Gateway / Auth Layer"]
        A2[Authenticate User]
        A1 --> A2
    end

    subgraph Router["🧭 Tenant Router Service"]
        A3[Lookup tenant_id → shard info]
        A2 --> A3
        A3 -->|Returns: shard_2, us-east-db02| A4
    end

    subgraph ShardLayer["🗂️ Database Shards (Horizontal Scaling)"]
        subgraph Shard1["Shard 1 (India-East)"]
            S1A[Partition: leads_2025_q1]
            S1B[Partition: contacts_2025_q1]
        end
        subgraph Shard2["Shard 2 (US-East)"]
            S2A[Partition: leads_2025_q1]
            S2B[Partition: leads_2025_q2]
            S2C[Partition: contacts_2025_q1]
        end
        subgraph Shard3["Shard 3 (Europe)"]
            S3A[Partition: leads_2025_q1]
        end
    end

    A4[Query Routed to Shard 2] --> S2A
    A4 --> S2B
    A4 --> S2C

    classDef shard fill:#e8f5e9,stroke:#2e7d32,color:#1b5e20,stroke-width:1px;
    classDef router fill:#fff3e0,stroke:#ef6c00,color:#e65100,stroke-width:1px;
    classDef gateway fill:#e3f2fd,stroke:#1976d2,color:#0d47a1,stroke-width:1px;
    classDef client fill:#f3e5f5,stroke:#6a1b9a,color:#4a148c,stroke-width:1px;

    class A1 client
    class A2 gateway
    class A3,A4 router
    class S1A,S1B,S2A,S2B,S2C,S3A shard
```

### 🧩 Explanation

1. **Client Request:**  
    The user’s request includes a `tenant_id`.
    
2. **Gateway Layer:**  
    Authenticates the user and forwards the request to the Tenant Router.
    
3. **Tenant Router Service:**
    
    - Maintains a mapping of each tenant to its shard.
        
    - Example:
        ``` 
        tenant_id | shard_id | db_host
		-----------|-----------|---------
		15422 | shard_2 | us-east-db02.zoho.com
        ```
        
        
    - Returns shard info to the backend.
        
4. **Shard Layer:**
    
    - Each shard is a separate database or cluster.
        
    - Within each shard, data is **partitioned** (by date, module, etc.) for performance.
        
5. **Query Execution:**
    
    - The backend connects directly to that shard’s DB.
        
    - Queries only relevant partitions.
        

---

### ⚡ Benefits

- **Scalable:** Each shard holds only a subset of tenants.
    
- **Efficient:** Partitions speed up local queries.
    
- **Isolated:** If one shard goes down, others stay unaffected.
    
- **Flexible:** Easy to add new shards or move tenants between shards.