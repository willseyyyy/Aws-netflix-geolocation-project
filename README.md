# AWS Netflix Geolocation Project

A fully implemented, production‑style AWS networking project demonstrating **Route 53 Geolocation Routing**, **multi‑region VPC design**, **EC2 web servers**, **Elastic IPs**, **Apache hosting**, and **custom front‑end templates** for India, USA, and Default/Service‑Unavailable locations.

This README is designed for **college submission, viva, resumes, and GitHub portfolio** — extremely detailed and formatted professionally.

---

# 📌 Table of Contents
1. Project Overview  
2. High‑Level Architecture  
3. AWS Services Used  
4. Network Layout  
5. VPC 1 — India (Mumbai Region)  
6. VPC 2 — USA (Northern Virginia Region)  
7. Service-Unavailable Server  
8. Route 53 Hosted Zone & DNS Configuration  
9. Geolocation Routing Logic  
10. Web Server Setup (Apache)  
11. Project File Structure  
12. Testing & Verification  
13. Screenshots to Include  
14. GitHub Deployment Instructions  
15. Viva / Interview Answers  
16. Conclusion  

---

# 📘 Project Overview
This project simulates a **Netflix‑style global content delivery system**, where users from different countries receive different homepage content.

Using **AWS Route 53 Geolocation routing**, the DNS automatically sends:
- Indian users → India EC2 server
- US users → USA EC2 server
- All other countries → Default 503 Service Unavailable page

Route 53 always routes based on **client IP location**, not EC2 region.

---

# 🏗 High-Level Architecture

```
User Request
     │
     ▼
Route 53 Hosted Zone (net-flix.xyz)
     │ Geolocation DNS Routing
     ├── India → 13.204.171.18
     ├── USA → 3.6.213.36
     └── Others → 13.204.244.22
     │
     ▼
EC2 Web Servers (Apache)
```

---

# 🧩 AWS Services Used

| Service | Purpose |
|--------|---------|
| VPC | Custom networks (India / USA) |
| Subnets | Public subnets |
| IGW | Internet connectivity |
| Route Tables | 0.0.0.0/0 → IGW |
| EC2 | Web servers |
| Elastic IP | Static global IP |
| Security Groups | Firewall rules |
| Route 53 | Geolocation routing |
| NetworkGeek DNS | NS record pointing |

---

# 🌐 Network Layout

## VPC 1 — India (Mumbai)
```
CIDR: 10.1.0.0/16
Subnet: 10.1.1.0/24
EC2 (India): 10.1.1.4 → 13.204.171.18
EC2 (Default): 10.1.1.5 → 13.204.244.22
```

## VPC 2 — USA (Virginia)
```
CIDR: 10.2.0.0/16
Subnet: 10.2.1.0/24
EC2 (USA): 10.2.1.4 → 3.6.213.36
```

---

# 🇮🇳 VPC 1 (India – Mumbai Region)

| Component | Name |
|----------|------|
| VPC | India-DC-VPC |
| Subnet | India-DC-Public-Subnet-AZ1 |
| IGW | India-DC-IGW |
| Route Table | India-DC-Public-RT |
| EC2 | Netflix-India-Server-1 |
| Elastic IP | 13.204.171.18 |

---

# 🇺🇸 VPC 2 (USA – Northern Virginia)

| Component | Name |
|----------|------|
| VPC | UC-DC-VPC |
| Subnet | US-DC-Public-Subnet-AZ1 |
| IGW | US-DC-IGW |
| EC2 | Netflix-US-Server-1 |
| Elastic IP | 3.6.213.36 |

---

# 🚫 Service-Unavailable Server
- Private IP: 10.1.1.5  
- Elastic IP: 13.204.244.22  
- Displays: 503 Service Unavailable

---

# 🧭 Route 53 Hosted Zone & DNS

### A Records (Geolocation Policy)

| Name | Country | IP |
|------|----------|------|
| www | India | 13.204.171.18 |
| www | United States | 3.6.213.36 |
| www | Default | 13.204.244.22 |

---

# 🌍 Geolocation Routing Logic

```
If India → India server
If USA → USA server
Else → Default server
```

---

# 🌐 Web Server Setup (Apache)

```
sudo apt update -y
sudo apt install apache2 -y
cd /var/www/html
sudo chmod 777 index.html
sudo nano index.html
```

Each server contains:
- india/index.html  
- usa/index.html  
- service-unavailable/index.html  

---

# 📁 Project File Structure

```
aws-netflix-geolocation-project/
├── india/
│   └── index.html
├── usa/
│   └── index.html
├── service-unavailable/
│   └── index.html
├── screenshots/
│   ├── india.png
│   ├── usa.png
│   ├── default.png
│   ├── route53.png
│   └── architecture.png
└── README.md
```

---

# 🧪 Testing & Verification

### Global tests used:
- GeoPeeker
- Uptrends
- WebPageTest

### Example DNS test:
```
nslookup www.<id>.net-flix.xyz 8.8.8.8
```

---

# 🖼 Screenshots to Include
- India homepage  
- USA homepage  
- Default 503 page  
- EC2 dashboard  
- Route 53 A records  
- VPC diagram  
- Ping tests from different regions  

---

# 📤 GitHub Deployment Instructions

```
git clone https://github.com/<username>/aws-netflix-geolocation-project.git
cd aws-netflix-geolocation-project
git add .
git commit -m "AWS Netflix Geolocation Project"
git push origin main
```
---

# 🏁 Conclusion
This project demonstrates:
- Multi‑VPC networking  
- Global DNS routing  
- Apache web hosting  
- Real-world OTT-style traffic routing  

Perfect for submissions, resumes, and interviews.

