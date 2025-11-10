---
date: 2025-11-09
tags:
link:
---
# 🌍 Redis Geospatial Index — Overview

Redis supports **geospatial indexing**, allowing you to store and query **latitude and longitude** data efficiently — for example, to find nearby locations such as stores, users, or delivery agents.

---

## 🧠 Requirements
- **Redis server** (version ≥ 6.2 recommended)
- A **dataset** containing latitude and longitude
- A **Redis client library** for your programming language (Java, Node.js, Python, etc.)

---

## ⚙️ How It Works

Redis stores geospatial data using a **sorted set (zset)** under the hood.  
Each location is stored as a *member* with a **geohash** as its score.

| Command | Purpose |
|----------|----------|
| `GEOADD` | Add location data |
| `GEOPOS` | Get the coordinates of a member |
| `GEODIST` | Calculate distance between two members |
| `GEOSEARCH` / `GEOSEARCHSTORE` | Find or store nearby locations |

---

## 🧩 Process

### 1. Upload / Store Data in Redis

You must **upload or insert** your geospatial data into Redis.

Example (CLI):
```bash
GEOADD locations 77.5946 12.9716 "Bangalore"
GEOADD locations 72.8777 19.0760 "Mumbai"
GEOADD locations 88.3639 22.5726 "Kolkata"
```
- `locations` → Redis key (the dataset)
    
- Each entry = longitude latitude name
    

---

### 2. Query Nearby Locations

Find all locations within a radius of a given point:

```
GEOSEARCH locations FROMLONLAT 77.6 12.9 BYRADIUS 500 km
```

This finds all entries within **500 km** of the given coordinates.

---
### 3. Query by Member

You can also find locations near an existing member:

`GEOSEARCH locations FROMMEMBER "Bangalore" BYRADIUS 500 km`

---

### 4. Store Query Results (Optional)

Use `GEOSEARCHSTORE` to store search results in another key:

`GEOSEARCHSTORE nearby_cities locations FROMMEMBER "Bangalore" BYRADIUS 500 km`

This creates a new key `nearby_cities` containing the results.

---

### 5. Get Distance Between Two Locations

`GEODIST locations Bangalore Mumbai km`

---

## ⚡ Behind the Scenes

Redis uses:

- **Geohash encoding** → to map coordinates to a single number
    
- **Sorted sets (zset)** → for efficient range querying
    

Results can include:

- Sorted nearest results
    
- Distances
    
- Coordinates
    
- Hashes
    

---

## 💡 Common Use Cases

- Finding nearest stores / ATMs / delivery drivers
    
- Location-based recommendations
    
- Geo-fencing or proximity alerts
    
- Real-time location tracking systems
    

---

## 🧠 Example Integration (Node.js)

``` node

await redis.geoadd('places', 77.5946, 12.9716, 'Bangalore'); const nearby = await redis.geosearch('places', 'FROMLONLAT', 77.6, 12.9, 'BYRADIUS', 100, 'km'); console.log(nearby);
```

## 📦 Data Persistence Strategy

- **Option 1:** Preload locations from your main DB (e.g., PostgreSQL, MongoDB) into Redis
    
- **Option 2:** Dynamically insert new data into Redis whenever new locations are created
    

Redis stores data in memory → extremely fast for real-time geolocation queries.



## 🔖Implementation
* [Redis geospatial with Springboot](https://github.com/sunil-kannan/Spring-with-Redis-Cache)