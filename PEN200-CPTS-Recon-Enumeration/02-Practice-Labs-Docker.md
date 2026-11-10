# 🧪 Practice Labs: Service Enumeration & Reconnaissance

Tập hợp các bài Lab containerized (Docker) mã nguồn mở trên GitHub để cày nát kỹ năng Enumeration theo đúng Runbook 5 bước.

---

## 1. Offensive Pentesting Lab (Đầy đủ nhất - Khuyên dùng)
* **GitHub Repository:** [InfoSecWarrior/Offensive-Pentesting-Lab](https://github.com/InfoSecWarrior/Offensive-Pentesting-Lab)
* **Các dịch vụ thực hành:**
  * **Port 53 (DNS):** Dò tìm bản ghi, Zone Transfer.
  * **Port 21 (FTP):** Anonymous login, rò rỉ file.
  * **Port 25 (SMTP):** VRFY user enumeration qua `smtp-user-enum`.
  * **Port 139 / 445 (SMB):** Null session, share permissions qua `smbmap` và `smbclient`.
  * **Port 161/udp (SNMP):** Dump OID/MIB, community strings `public` qua `snmp-check`.
  * **Port 80 / 443 (Web):** Directory fuzzing qua `gobuster`, quét CVE qua `nuclei`.

### Cách chạy nhanh trên Kali:
```bash
git clone https://github.com/InfoSecWarrior/Offensive-Pentesting-Lab.git
cd Offensive-Pentesting-Lab
sudo docker compose up -d
sudo docker compose ps
```

---

## 2. Ethical Hacking Docker Labs (12 Bài chuẩn chỉnh)
* **GitHub Repository:** [michael-borck/ethical-hacking-docker-labs](https://github.com/michael-borck/ethical-hacking-docker-labs)
* **Nội dung:**
  * Lab 1-3: Network scanning & Host discovery (Nmap Ping sweeps, TCP/UDP scanning).
  * Lab 4-6: Service enumeration chuyên sâu từng giao thức.
  * Lab 7-9: Password auditing & Exploitation.

---

## 3. Vulhub (Kho thực tế 200+ CVE)
* **GitHub Repository:** [vulhub/vulhub](https://github.com/vulhub/vulhub)
* Chuyên dùng để test Nuclei templates và Nmap NSE `--script vuln`.
