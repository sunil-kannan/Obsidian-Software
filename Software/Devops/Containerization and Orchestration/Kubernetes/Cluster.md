---
date: "2025-10-25"
tags: 
link:
---

# Cluster

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

  
i run external LBs F5 (on prem) or azure LB (2) in front of 3 infra nodes running haproxy. worker nodes separate.

all of our ocp, master, infra , and workers are airgapped.

in front of the external LBs is network dmz (more LB), waf etc etc.



An F5 load balancer is ==a network device or software from F5, Inc. that distributes network traffic across multiple servers to improve application availability, performance, and reliability==. Key F5 load balancing solutions include the [BIG-IP](https://www.google.com/search?q=BIG-IP&sca_esv=539feba37f4d5ea0&ei=7yf8aKmRCLeSseMPlrSD6AE&oq=f5&gs_lp=Egxnd3Mtd2l6LXNlcnAiAmY1KgIIADIQEAAYgAQYsAMYsQMYQxiKBTINEAAYgAQYsAMYQxiKBTINEAAYgAQYsAMYQxiKBTINEAAYgAQYsAMYQxiKBTINEAAYgAQYsAMYQxiKBTINEAAYgAQYsAMYQxiKBTIJEAAYsAMYBxgeMhMQABiABBiwAxixAxhDGIMBGIoFMg0QABiABBiwAxhDGIoFMg0QABiABBiwAxhDGIoFMgkQABiwAxgHGB4yDRAAGIAEGLADGEMYigUyDhAAGLADGOQCGNYE2AEBMg4QABiwAxjkAhjWBNgBATIOEAAYsAMY5AIY1gTYAQEyHxAuGIAEGLADGLEDGNEDGEMYgwEYxwEYyAMYigXYAQEyFhAuGIAEGLADGEMY5QQYyAMYigXYAQEyFhAuGIAEGLADGEMY5QQYyAMYigXYAQEyFhAuGIAEGLADGEMY5QQYyAMYigXYAQFI3gxQAFgAcAF4AJABAJgBAKABAKoBALgBAcgBAJgCAaACB5gDAIgGAZAGE7oGBggBEAEYCZIHATGgBwCyBwC4BwDCBwMyLTHIBwY&sclient=gws-wiz-serp&ved=2ahUKEwiP3ujHmb6QAxV4zzgGHXjsKXMQgK4QegYIAQgAEAY) family for integrated traffic management and security, and NGINX for high-traffic websites. They work by intelligently routing incoming requests to the most suitable server and can also provide advanced features like health monitoring, security, and global server load balancing (GSLB).