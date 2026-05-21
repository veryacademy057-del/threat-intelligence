# 🕵️ Threat Intelligence Tools — OSINT untuk Investigasi Ancaman

> **Seri Lab:** Blue Team SOC Lab  
> **Platform:** [TryHackMe](https://tryhackme.com)  
> **YouTube:** [▶️ Tonton Tutorial di YouTube](https://youtu.be/3xFl2SPDKl0?si=V6XUciPz4bwTzAIS)  
> **Kategori:** `Threat Intelligence, OSINT, Email Analysis`

---

## 📋 Deskripsi

Lab ini memperkenalkan berbagai **OSINT tools** yang digunakan SOC Analyst untuk melakukan threat assessment dan investigasi ancaman. Mulai dari scanning URL berbahaya, tracking malware & botnet, analisis email phishing, hingga intel gathering menggunakan platform Cisco Talos.

---

## 🎬 Video Tutorial

[![Threat Intelligence Tools - OSINT Investigation](https://img.youtube.com/vi/3xFl2SPDKl0/maxresdefault.jpg)](https://youtu.be/3xFl2SPDKl0?si=V6XUciPz4bwTzAIS)

> 📺 **[Tonton di YouTube → Threat Intelligence Tools: OSINT untuk Investigasi Ancaman](https://youtu.be/3xFl2SPDKl0?si=V6XUciPz4bwTzAIS)**

---

## 🧠 Apa itu Threat Intelligence?

**Threat Intelligence** adalah analisis data dan informasi menggunakan tools dan teknik untuk menghasilkan pola bermakna tentang cara memitigasi risiko dari ancaman yang ada maupun yang baru muncul.

**Pertanyaan yang dijawab oleh Threat Intelligence:**

| Pertanyaan | Keterangan |
|------------|------------|
| Siapa yang menyerang? | Identitas atau grup threat actor |
| Apa motivasinya? | Finansial, spionase, aktivisme, dll |
| Apa kapabilitasnya? | Tools, teknik, dan prosedur yang digunakan |
| Artefak apa yang harus diwaspadai? | IoC — IP, domain, hash, URL berbahaya |

---

## 🗂️ Klasifikasi Threat Intelligence

| Tipe | Penjelasan |
|------|------------|
| **Strategic Intel** | High-level — gambaran besar lanskap ancaman untuk keputusan bisnis |
| **Technical Intel** | Bukti dan artefak serangan — digunakan untuk membangun baseline pertahanan |
| **Tactical Intel** | TTPs (Tactics, Techniques, Procedures) attacker — untuk memperkuat kontrol keamanan |
| **Operational Intel** | Motif dan niat spesifik attacker terhadap target tertentu |

---

## 🛠️ Tools yang Digunakan

| Tool | Fungsi Utama |
|------|-------------|
| **UrlScan.io** | Scan dan analisis URL mencurigakan |
| **Abuse.ch** | Tracking malware, botnet, dan IoC |
| **PhishTool** | Analisis email phishing secara mendalam |
| **Cisco Talos** | Intel gathering berbasis reputasi IP dan file |
| **VirusTotal** | Analisis hash file untuk identifikasi malware |

---

## 🌐 Tool 1 — UrlScan.io

**UrlScan.io** adalah layanan gratis untuk scanning dan analisis website secara otomatis. Saat URL disubmit, informasi yang direkam meliputi:

- Domain dan IP address yang dihubungi
- Resource yang diminta dari domain
- Screenshot halaman web
- Teknologi yang digunakan
- Metadata lainnya

### Tab Hasil Scan UrlScan.io

| Tab | Informasi |
|-----|-----------|
| **Summary** | IP address, detail registrasi domain, histori halaman, screenshot |
| **HTTP** | Koneksi HTTP yang dibuat scanner, data yang diambil, tipe file |
| **Redirects** | HTTP dan client-side redirect yang teridentifikasi |
| **Links** | Semua outgoing link dari homepage |
| **Behaviour** | Variabel dan cookie — berguna identifikasi framework |
| **Indicators** | Semua IP, domain, dan hash yang terasosiasi dengan site |

### Hasil Investigasi — TryHackMe Domain

| Field | Nilai |
|-------|-------|
| **Cisco Umbrella Rank** | `345612` |
| **Jumlah Domain Teridentifikasi** | `13` |
| **Domain Registrar** | `NAMECHEAP INC` |
| **IP Address Utama** | `2606:4700:10::ac43:1b0a` |

---

## 🦠 Tool 2 — Abuse.ch

**Abuse.ch** adalah research project dari Bern University of Applied Sciences, Swiss — dikembangkan untuk mengidentifikasi dan tracking malware serta botnet.

### Platform-Platform Abuse.ch

| Platform | Fungsi |
|----------|--------|
| **MalwareBazaar** | Database koleksi dan analisis malware — upload sampel, hunting dengan YARA rules |
| **FeodoTracker** | Tracking botnet C2 server (Dridex, Emotet, TrickBot, QakBot, BazarLoader) |
| **SSL Blacklist** | Identifikasi SSL certificate berbahaya dan JA3/JA3s fingerprint botnet C2 |
| **URLhaus** | Database URL distribusi malware — cari domain, URL, hash, filetype |
| **ThreatFox** | Berbagi dan export IoC dalam format MISP, Suricata rules, JSON, CSV |

### Hasil Investigasi Abuse.ch

| Pertanyaan | Platform | Jawaban |
|------------|----------|---------|
| Malware alias untuk IoC `212.192.246.30:5555` | ThreatFox | `Katana` |
| Malware untuk JA3 fingerprint `51c64c77e60f3980eea90869b68c58a8` | SSL Blacklist | `Dridex` |
| Jaringan hosting malware dengan ASN `AS14061` | URLhaus | `DIGITALOCEAN-ASN` |
| Negara untuk botnet IP `178.134.47.166` | FeodoTracker | `Georgia` |

---

## 📧 Tool 3 — PhishTool

**PhishTool** adalah tool analisis email phishing yang mengekstrak metadata dan memberikan kemampuan investigasi mendalam terhadap email mencurigakan.

### Fitur Utama PhishTool

| Fitur | Penjelasan |
|-------|------------|
| **Email Analysis** | Mengambil metadata dari email phishing — attachment, URL, header |
| **Heuristic Intelligence** | OSINT terintegrasi untuk memahami TTP attacker |
| **Classification & Reporting** | Klasifikasi email phishing dan generate laporan forensik |

### Tab Analisis di PhishTool

| Tab | Informasi |
|-----|-----------|
| **Headers** | Routing email — source/destination, originating IP, timestamp |
| **Received Lines** | Jalur traversal email melalui berbagai SMTP server |
| **X-headers** | Extension header tambahan dari mailbox penerima |
| **Security** | Hasil SPF, DKIM, dan DMARC |
| **Attachments** | Daftar lampiran yang ditemukan |
| **Message URLs** | URL eksternal yang terdapat dalam email |

---

### Investigasi Email1.eml — LinkedIn Phishing

| Field | Nilai |
|-------|-------|
| **Platform yang Ditiru** | `LinkedIn` |
| **Email Pengirim** | `darkabutla@sc500.whpservers.com` |
| **Email Penerima** | `cabbagecare@hotsmail.com` |
| **Originating IP (Defanged)** | `204[.]93[.]183[.]11` |
| **Jumlah Hop** | `4` |

> 💡 **Defanging IP** adalah praktik standar SOC untuk menulis IP berbahaya dalam format yang tidak bisa diklik secara tidak sengaja — titik diganti `[.]`.

---

## 🔵 Tool 4 — Cisco Talos Intelligence

**Cisco Talos** adalah tim keamanan besar dari Cisco yang menyediakan threat intelligence berbasis data dari produk-produk Cisco di seluruh dunia.

### Enam Tim Utama Cisco Talos

| Tim | Fungsi |
|-----|--------|
| **Threat Intelligence & Interdiction** | Korelasi dan tracking ancaman — mengubah IoC menjadi intel kontekstual |
| **Detection Research** | Analisis malware dan kerentanan untuk membuat detection rules |
| **Engineering & Development** | Pemeliharaan inspection engine agar selalu up-to-date |
| **Vulnerability Research & Discovery** | Identifikasi dan pelaporan kerentanan ke vendor |
| **Communities** | Menjaga reputasi tim dan solusi open-source |
| **Global Outreach** | Menyebarkan intelligence ke pelanggan dan komunitas keamanan |

### Tab Utama di Talos Intelligence

| Tab | Informasi |
|-----|-----------|
| **Vulnerability Information** | CVE dan CVSS score, timeline publikasi, Snort rules |
| **Reputation Center** | Lookup reputasi IP dan file berdasarkan SHA256 hash |
| **Email & Spam Data** | Data email dan spam berdasarkan reputasi domain/IP |

---

## 🧪 Investigasi Skenario

### Skenario 1 — Email2.eml

| Field | Nilai |
|-------|-------|
| **Email Penerima** | `chris.lyons@supercarcenterdetroit.com` |
| **Tahun Pertama Submission di VirusTotal** | `2017` |

---

### Skenario 2 — Email3.eml

| Field | Nilai |
|-------|-------|
| **Nama Lampiran** | `Sales_Receipt 5606.xls` |
| **Malware Family** | `Dridex` |

> 💡 **Dridex** adalah banking trojan yang menyebar melalui email phishing berisi dokumen Office berbahaya. Dridex sering terdeteksi juga di SSL Blacklist dan FeodoTracker milik Abuse.ch.

---

## 🔄 Alur Investigasi Threat Intelligence

```
Indikator Mencurigakan (IP, URL, Hash, Email)
                │
                ▼
    ┌───────────────────────┐
    │  Apakah ini URL/Domain?│
    └───────────┬───────────┘
                │ Ya
                ▼
          UrlScan.io
          (Analisis website)
                │
    ┌───────────────────────┐
    │  Apakah ini Hash/File? │
    └───────────┬───────────┘
                │ Ya
                ▼
    MalwareBazaar / VirusTotal
    (Identifikasi malware family)
                │
    ┌───────────────────────┐
    │  Apakah ini IP/Domain? │
    └───────────┬───────────┘
                │ Ya
                ▼
  FeodoTracker / Talos / ThreatFox
  (Reputasi & botnet tracking)
                │
    ┌───────────────────────┐
    │  Apakah ini Email?     │
    └───────────┬───────────┘
                │ Ya
                ▼
          PhishTool
          (Analisis phishing)
```

---

## 📋 Ringkasan Tools & Kegunaannya

| Tool | Input | Output |
|------|-------|--------|
| **UrlScan.io** | URL | Screenshot, domain, IP, teknologi |
| **MalwareBazaar** | Hash / tag | Sampel malware, YARA rules |
| **FeodoTracker** | IP Address | Status botnet C2, negara, malware family |
| **SSL Blacklist** | JA3 fingerprint / SSL cert | Malware family yang menggunakan SSL tersebut |
| **URLhaus** | URL / domain / hash | Status malware hosting, ASN |
| **ThreatFox** | IP:Port / domain / hash | IoC, malware alias, export format |
| **PhishTool** | File .eml | Header, SPF/DKIM/DMARC, attachment, URL |
| **Cisco Talos** | IP / hash | Reputation score, CVE, Snort rules |
| **VirusTotal** | Hash / URL / file | Detection rate, first submission, behavior |

---

## 📌 Kesimpulan

| Poin | Penjelasan |
|------|------------|
| **Threat Intelligence** | Analisis data untuk menghasilkan intel yang dapat ditindaklanjuti |
| **OSINT Tools** | Mempercepat investigasi — IP, URL, hash, email bisa dicek dalam hitungan detik |
| **Defanging** | Praktik standar penulisan IoC berbahaya agar tidak bisa diklik |
| **Dridex** | Banking trojan populer yang terdeteksi di banyak platform (VirusTotal, Abuse.ch, SSL Blacklist) |
| **Kombinasi Tools** | Satu IoC sebaiknya dicek di beberapa platform untuk hasil yang komprehensif |

---

## 📚 Referensi

- [UrlScan.io](https://urlscan.io/)
- [Abuse.ch — MalwareBazaar](https://bazaar.abuse.ch/)
- [Abuse.ch — FeodoTracker](https://feodotracker.abuse.ch/)
- [Abuse.ch — SSL Blacklist](https://sslbl.abuse.ch/)
- [Abuse.ch — URLhaus](https://urlhaus.abuse.ch/)
- [Abuse.ch — ThreatFox](https://threatfox.abuse.ch/)
- [PhishTool Community](https://www.phishtool.com/)
- [Cisco Talos Intelligence](https://talosintelligence.com/)
- [VirusTotal](https://www.virustotal.com/)
- [MITRE ATT&CK — Threat Intelligence](https://attack.mitre.org/)

---

*📺 Ikuti tutorialnya di [YouTube](https://youtu.be/3xFl2SPDKl0?si=V6XUciPz4bwTzAIS) | ⭐ Star repo ini jika membantu!*
