# 🗺️ QUY TRÌNH ENUMERATION CHUẨN 5 BƯỚC (RUNBOOK THỰC CHIẾN RED TEAM / CPTS / OSCP)

> Tác giả: Nguyễn Duy Quang (HE181202)  
> Mục tiêu: Master giai đoạn Active Information Gathering & Service Enumeration  

---

```
[BƯỚC 1: CHECK THÔNG MẠNG]       ---> ping kiểm tra sống/chết & đoán OS qua TTL
              │
              ▼
[BƯỚC 2: QUÉT CỔNG (PORT SCAN)]  ---> Chạy 2 nhịp Nmap (Nhanh mặt tiền + Ngầm full port)
              │
              ▼
[BƯỚC 3: PHÂN LOẠI & ĐÁNH DỊCH VỤ]
  ├─ Thấy Port 445 (SMB)         ---> smbmap / smbclient / enum4linux-ng
  ├─ Thấy Port 2049 (NFS)        ---> showmount -e / mount
  ├─ Thấy Port 161/udp (SNMP)    ---> onesixtyone / snmp-check / snmpwalk
  ├─ Thấy Port 25 (SMTP)         ---> smtp-user-enum / VRFY
  └─ Thấy Port 80/443 (Web)      ---> nuclei / nikto / gobuster
              │
              ▼
[BƯỚC 4: TỔNG HỢP NGUYÊN LIỆU]    ---> Gom User list, Passwords, SSH keys, CVE versions
              │
              ▼
[BƯỚC 5: TẤN CÔNG (EXPLOITATION)] ---> Đăng nhập SSH/RDP HOẶC Bắn Exploit lấy Shell!
```

---

## 🟢 BƯỚC 1: KIỂM TRA THÔNG MẠNG & ĐOÁN OS (Mất 2 giây)
```bash
ping -c 2 <IP_MỤC_TIÊU>
```
* **Mắt nhìn cái gì?**
  * `ttl=64` (hoặc 63) $\rightarrow$ Hệ điều hành **Linux**.
  * `ttl=128` (hoặc 127) $\rightarrow$ Hệ điều hành **Windows**.
  * Nếu không có phản hồi ICMP $\rightarrow$ Server chặn Ping, bắt buộc thêm cờ `-Pn` vào mọi lệnh Nmap.

---

## 🟢 BƯỚC 2: QUÉT CỔNG BẰNG NMAP (Chiến thuật 2 nhịp)

* **Tab 1 (Mặt tiền - Có kết quả sau 5 giây để làm việc ngay):**
  ```bash
  sudo nmap -sC -sV <IP_MỤC_TIÊU> -oN quick_scan.txt
  ```
* **Tab 2 (Chạy ngầm dưới nền - Quét sạch 65.535 cổng đề phòng cổng dị):**
  ```bash
  sudo nmap -sS -p- --min-rate 1000 -Pn <IP_MỤC_TIÊU> -oN full_ports.txt > /dev/null 2>&1 &
  ```

---

## 🟢 BƯỚC 3: MA TRẬN ĐÁNH CỔNG DỊCH VỤ (THẤY CỔNG NÀO - BẮN CỔNG ĐÓ)

### 🔹 1. Port 445 (SMB) - Windows / Samba
* **Mục tiêu:** Tìm file backup, lộ password, đào danh sách User.
```bash
# 1. Soi quyền các share folder (tìm cái nào READ ONLY / READ WRITE)
smbmap -H <IP_MỤC_TIÊU>

# 2. Chui vào share folder tải file về (cờ -N là không mật khẩu)
smbclient //<IP_MỤC_TIÊU>/<tên_share> -N

# 3. Vét cạn thông tin và danh sách User qua RID cycling
enum4linux-ng -A <IP_MỤC_TIÊU>
```

### 🔹 2. Port 2049 / 111 (NFS) - Network File System
* **Mục tiêu:** Mount ổ đĩa Linux về máy Kali để lấy cắp SSH Key (`id_rsa`) hoặc ghi đè `authorized_keys`.
```bash
# 1. Xem server đang share thư mục nào
showmount -e <IP_MỤC_TIÊU>

# 2. Tạo thư mục tạm trên Kali và gắn về
sudo mkdir -p /tmp/nfs
sudo mount -t nfs -o nolock <IP_MỤC_TIÊU>:/<thư_mục_share> /tmp/nfs

# 3. Vào lục lọi file
cd /tmp/nfs && ls -la
```

### 🔹 3. Port 161 UDP (SNMP) - Mỏ vàng giám sát
* **Mục tiêu:** Rút cạn danh sách User, tiến trình chạy ngầm, card mạng nội bộ.
```bash
# 1. Dò Community String mặc định (public / private)
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt <IP_MỤC_TIÊU>

# 2. Dùng snmp-check đọc sạch toàn bộ báo cáo phân loại
snmp-check <IP_MỤC_TIÊU> -c public
```

### 🔹 4. Port 25 (SMTP) - Mail Server
* **Mục tiêu:** Xác minh xem những User nào có thật trên hệ thống để làm nguyên liệu brute-force.
```bash
smtp-user-enum -M VRFY -U /usr/share/wordlists/seclists/Usernames/top-usernames-shortlist.txt -t <IP_MỤC_TIÊU>
```

### 🔹 5. Port 80 / 443 (HTTP / HTTPS) - Web Applications
* **Mục tiêu:** Tìm thư mục ẩn, file backup, trang admin, lỗi CVE.
```bash
# 1. Quét lỗi nhanh bằng Nuclei (Template cộng đồng)
nuclei -u http://<IP_MỤC_TIÊU>

# 2. Quét tìm thư mục và file ẩn (.php, .txt, .bak)
gobuster dir -u http://<IP_MỤC_TIÊU> -w /usr/share/wordlists/dirb/common.txt -x php,txt,bak,html -t 30
```

---

## 🟢 BƯỚC 4: TỔNG HỢP NGUYÊN LIỆU (THE LOOT)
Gom toàn bộ dữ liệu nhặt được:
* Danh sách **Usernames** (từ SMB, SMTP, SNMP).
* Mật khẩu lộ thiên (từ file `notes.txt`, file backup `.sql`, config).
* Khóa bảo mật **SSH Private Key (`id_rsa`)**.

---

## 🟢 BƯỚC 5: TẤN CÔNG ĐỔI LẤY SHELL (EXPLOITATION)
* Dùng User + Pass đăng nhập SSH: `ssh user@<IP_MỤC_TIÊU>`
* Dùng SSH Key: `chmod 600 id_rsa && ssh -i id_rsa user@<IP_MỤC_TIÊU>`
* $\rightarrow$ **CÓ NGAY SHELL ĐẦU TIÊN (INITIAL FOOTHOLD)!**
