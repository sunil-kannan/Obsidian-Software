---
date: "2025-10-26"
tags: 
link:
---

# 🔐 Signed URL — Secure Media Delivery Notes

## 📘 What is a Signed URL?

A **Signed URL** (also called a *Pre-signed URL* or *Tokenized URL*) is a **temporary, access-controlled link** to a protected resource such as a video, image, or file on a CDN or storage system.

It allows authorized users or applications to **access a file without exposing permanent credentials**.

---

## ⚙️ How It Works (Concept Overview)

1. **User / Client requests access**
   - The app asks the backend for a resource (e.g., video or image).
2. **Backend checks permissions**
   - The server verifies the user’s authentication and authorization (e.g., follower status, privacy settings, paid subscription).
3. **Backend generates a signed URL**
   - The server creates a **temporary URL** that includes:
     - File path  
     - Expiration time  
     - Cryptographic signature (HMAC or token)
4. **Client uses the signed URL**
   - The client app or browser fetches the file **directly from the CDN or storage** using the signed URL.
5. **CDN validates the signature**
   - The CDN checks if the URL’s signature and expiry are valid.
   - If valid → content served  
     If invalid/expired → returns `403 Forbidden`.

---

## 🔑 Components of a Signed URL

| Field | Description | Example |
|--------|--------------|----------|
| **Base URL** | The file or CDN path | `https://cdn.example.com/video.mp4` |
| **Expiry timestamp** | When the link expires | `Expires=1735260000` |
| **Access key ID / token ID** | Identifies which key was used | `KeyID=ABCD1234` |
| **Signature** | Cryptographic proof using a secret key | `Signature=a94f...xyz` |
| **Optional constraints** | IP, referer, user ID | `IP=203.0.113.1` |

### Example:
```
https://cdn.example.com/video.mp4?Expires=1735260000&Signature=abc123xyz&KeyID=myKey
```

---

## 🧮 Signature Generation (Simplified)

Most systems use **HMAC-SHA256** to sign the URL:

```
signature = HMAC(secret_key, string_to_sign)
string_to_sign = path + expiry + parameters


The resulting `signature` is appended as a query parameter.
```

---

## ⏳ Expiration

- Signed URLs are valid **only for a short duration** (e.g., 1–10 minutes).
- Once expired, the CDN will reject the request.
- Apps must request a new signed URL from the backend if they reload the resource.

This ensures that even if the link leaks, it becomes **useless after expiry**.

---

## 🏗️ Why Use Signed URLs

| Benefit | Explanation |
|----------|--------------|
| **Security** | Prevents direct or permanent access to private files. |
| **Scalability** | Offloads serving of files to CDNs or object storage. |
| **Performance** | CDN can serve files directly without app-level permission checks. |
| **Access Control** | Backend ensures only authorized users receive valid URLs. |
| **Auditability** | Each URL can be tied to a user or session. |

---

## 🚫 What Signed URLs Do *Not* Do

- They **don’t check business logic** like “is this user following that person?”  
  → That check happens **before** the URL is issued.  
- They **don’t authenticate users** directly — they rely on a trusted backend to do that first.
- They **don’t persist indefinitely** — they expire and must be refreshed.

---

## 📦 Common Use Cases

| Platform | Example Usage |
|-----------|----------------|
| **AWS S3** | `s3.getSignedUrl('getObject', { Bucket, Key, Expires })` |
| **Google Cloud Storage** | `generate_signed_url()` for temporary download/upload |
| **CloudFront CDN** | Signed URLs and Signed Cookies for private content |
| **TikTok / Instagram / YouTube** | Serve user-specific, time-limited video URLs after verifying permissions |
| **Private APIs** | Temporary download links for PDFs, images, etc. |

---

## 🧠 Real-World Example — TikTok / Instagram Private Video

1. You request a private user’s post.  
2. Backend verifies your **auth token** and **follower relationship**.  
3. If allowed, backend issues a **short-lived signed CDN URL** for that video.  
4. App fetches the video directly from CDN.  
5. The CDN validates the signature and serves the video.  

If you copy that URL and share it:
- It’ll expire within minutes, or  
- It’s bound to your session/IP, so others can’t use it.

Thus, **access remains secure and controlled**, even though CDN URLs are publicly visible.

---

## 🔍 CDN’s Role vs Backend’s Role

| Step | Actor | Responsibility |
|------|--------|----------------|
| 1️⃣ | **Backend (App Server)** | Authenticates user, checks access rules |
| 2️⃣ | **Backend** | Generates signed URL |
| 3️⃣ | **Client** | Uses signed URL to fetch resource |
| 4️⃣ | **CDN / Storage** | Verifies signature and expiry only |
| 5️⃣ | **CDN** | Serves or denies the content |

**Important:** The CDN does *not* check “follower” or “permission” logic — it only validates the cryptographic token.

---

## ⚙️ Common Parameters Used in Signed URLs

| Parameter | Purpose |
|------------|----------|
| `Expires` | Unix timestamp for expiry |
| `Signature` | HMAC hash or encrypted token |
| `KeyID` | Identifies signing key |
| `Policy` | Optional JSON defining constraints |
| `IP` | Restricts to a specific client IP |
| `URL` / `Resource` | Path to the file or resource |

---

## 🧾 Summary

- **Signed URLs** = Temporary, secure, tokenized links to restricted files.  
- **Backend handles authorization** → **CDN handles fast delivery**.  
- **Used heavily** in modern apps like TikTok, Instagram, YouTube, and cloud storage systems.  
- **Best practice:** Keep expiration short (minutes) and regenerate on each session.


