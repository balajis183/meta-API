## ✅ Domain Configuration Report: `bluebex.xyz`

### ✅ Current Setup Overview

- **Domain Registrar:** GoDaddy  
- **Hosting:** AWS EC2 with Application Load Balancer (ALB)  
- **Elastic IP:** `15.206.226.196`  
- **SSL Certificate:** Issued via AWS ACM and attached to ALB  
- **ALB DNS Name:** `bluebex-server-ALB-1294013851.ap-south-1.elb.amazonaws.com`

---

### 🛠️ DNS Records (GoDaddy)

| Type     | Host | Points To / Value                                              | Purpose                                      |
|----------|------|----------------------------------------------------------------|----------------------------------------------|
| A        | @    | `15.206.226.196`                                               | Root domain (http only for now)              |
| CNAME    | www  | `bluebex-server-ALB-1294013851.ap-south-1.elb.amazonaws.com`   | Subdomain routed via ALB with SSL            |
| ❌Remove | www  | `15.206.226.196`                                               | Was pointing to IP – **should be removed**   |

---

### ⚠️ Important Notes

- The ALB DNS name is not an IP address, so **it cannot be used in an A record** — it must be used with a **CNAME**.
- The **A record for `www` pointing to the IP should be removed**, or it may conflict with the CNAME.
- Only `www.bluebex.xyz` is currently using **HTTPS via ALB**. The root domain (`bluebex.xyz`) still routes directly to the EC2 instance.
