# Security Study Portfolio

> Ghi chép quá trình tự học **Cyber Security** — hướng **SOC Tier 3** & **OSCP Prep**.  
> Bởi **Nguyễn Duy Quang** (HE181202) — Sinh viên năm 4, FPT University Hà Nội.

---

## Giới thiệu

Repository này lưu lại toàn bộ kiến thức, ghi chú, và bài tập thực hành trong quá trình ôn luyện.  
Học đến đâu — đẩy đến đó. Không có nội dung placeholder.

**Định hướng:**
- Lộ trình SOC Tier 3 (Incident Responder / Threat Hunter)
- Ôn tập OSCP (4-Week Prep Plan)
- Application Security

---

## Roadmap & Tiến độ

### CyberJutsu Courses
| Khóa học | Trạng thái | Ghi chú |
|:---|:---:|:---|
| Web Penetration Testing 101 | ⬜ | — |
| Web Penetration Testing 102 | ⬜ | — |
| CVE Analysis | ⬜ | — |
| Web Pentest (Demo) | ⬜ | — |

### OSCP Prep — Tuần 1: Networking & Linux CLI
| Chủ đề | Trạng thái | Tài liệu |
|:---|:---:|:---|
| L1 — Physical Layer | ✅ Xong | [L1-Physical-Layer.md](Week-01-Networking/L1-Physical-Layer.md) |
| L2 — Data Link Layer | ✅ Xong | [L2-Data-Link-Layer.md](Week-01-Networking/L2-Data-Link-Layer.md) |
| L3 — Network (IP, ICMP, Subnetting) | ✅ Xong | [L3-Network-Layer.md](Week-01-Networking/L3-Network-Layer.md) |
| L4 — Transport (TCP, UDP, Flow Control) | ✅ Xong | [L4-Transport-Layer.md](Week-01-Networking/L4-Transport-Layer.md) |
| L5 — Session | ✅ Xong | [L5-Session-Layer.md](Week-01-Networking/L5-Session-Layer.md) |
| L6 — Presentation | ✅ Xong | [L6-Presentation-Layer.md](Week-01-Networking/L6-Presentation-Layer.md) |
| L7 — Application (HTTP, DNS, DHCP, FTP) | ✅ Xong | [L7-Application-Layer.md](Week-01-Networking/L7-Application-Layer.md) |
| Networking Interview Cheatsheet | ✅ Xong | [Networking-Interview-Cheatsheet.md](Week-01-Networking/Networking-Interview-Cheatsheet.md) |
| Linux CLI (permissions, pipes, SUID, awk/sed) | ✅ Xong | [Linux-CLI-For-Hackers.md](Week-01-Networking/Linux-CLI-For-Hackers.md) |

### OSCP Prep — Tuần 2: Coding & SQL Injection
| Chủ đề | Trạng thái | Tài liệu |
|:---|:---:|:---|
| Python & Exploit Code Reading | ⬜ | — |
| Bash Scripting (ping sweep, port scanner) | ⬜ | — |
| SQL & SQLi (Union, Blind, scripting) | ⬜ | — |

### OSCP Prep — Tuần 3: Recon & Web Exploitation
| Chủ đề | Trạng thái | Tài liệu |
|:---|:---:|:---|
| Recon & Enumeration 5-Step Runbook (DNS, Nmap, SMB, NFS, SMTP, SNMP, Vuln Scan) | ✅ Xong | [01-Enumeration-Runbook-5-Steps.md](PEN200-CPTS-Recon-Enumeration/01-Enumeration-Runbook-5-Steps.md) |
| Practice Labs (Docker Hub & GitHub Labs for Recon) | ✅ Xong | [02-Practice-Labs-Docker.md](PEN200-CPTS-Recon-Enumeration/02-Practice-Labs-Docker.md) |
| Web Exploitation (LFI/RFI, Log Poisoning, File Upload, SQLi) | ⏳ Đang học | — |
| Win32 Buffer Overflow | ⬜ | — |

### OSCP Prep — Tuần 4: Mock Tests & Interview
| Chủ đề | Trạng thái | Tài liệu |
|:---|:---:|:---|
| HTB/TryHackMe Box Methodology | ⬜ | — |
| Interview Prep (IR logic, personal intro) | ⬜ | — |

---

## Cấu trúc thư mục

```
.
├── README.md
└── Week-01-Networking/
    ├── L1-Physical-Layer.md
    ├── L2-Data-Link-Layer.md
    ├── L3-Network-Layer.md
    ├── L4-Transport-Layer.md
    ├── L5-Session-Layer.md
    ├── L6-Presentation-Layer.md
    ├── L7-Application-Layer.md
    ├── Linux-CLI-For-Hackers.md
    └── Networking-Interview-Cheatsheet.md
```

> Thư mục mới sẽ được thêm theo tiến trình học.

---

## Background

- **Thực tập:** V2Secure. Xuất phát điểm ở Phòng Hạ tầng, đóng vai trò **Pioneer** xây dựng quy trình SOC (Incident Response, Forms).
- **Kinh nghiệm:** Monitor Health/Security (ESXi, 2x WAF, SIEM, PAM, NIPS). Có kỹ năng viết script tự động hóa (PowerShell MD5/DNS Resolver).
- **Chuyên môn Sâu:** Malware Analysis (CAPE Sandbox, FLARE VM, REMnux, Ghidra, Volatility 3) và Network Routing/Switching (CCNA v7 Packet Tracer Labs).
- **Công cụ thường dùng:** Wireshark, Nmap, Burp Suite, Python, Linux CLI.

---

*Cập nhật lần cuối: 2026-07-09*
