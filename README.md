# 🚀 V2Ray Tester - Termux (Pro Version)

Alat pengujian otomatis berbasis Python untuk memvalidasi konfigurasi **VMess / WebSocket / TLS / SNI** langsung di dalam lingkungan **Termux**. Dirancang khusus agar struktur pengujiannya selaras dengan standar aplikasi **v2rayNG**.

---

## ✨ Fitur Utama

- **Kompatibel V2Ray Core v5.x**: Menggunakan binary V2Ray Core terbaru yang stabil.
- **Auto IP Resolver**: Otomatis menerjemahkan domain ke IP di sisi Python untuk memutus error DNS khas Termux (`lookup [::1]:53 connection refused`).
- **Validasi Konten Ketat**: Menganalisis isi bodi Cloudflare Trace untuk mengeliminasi *false positive* (seperti halaman jebakan/redirect operator seluler).
- **Pengujian Multi-Metode**: Mendukung pengujian metode `ADDRESS`, `WS_HOST`, dan `SNI`.
- **Export Laporan JSON**: Menyimpan ringkasan pengujian ke `response.json` untuk diintegrasikan dengan alat lain.

---

## 📦 Panduan Instalasi (Langkah Demi Langkah)

Jalankan perintah-perintah berikut di aplikasi Termux Anda:

### 1. Update Termux & Install Dependensi Utama
```bash
pkg update && pkg upgrade -y
pkg install python curl wget unzip micro -y

git clone https://github.com/Alamyazid/tester_bug_v2ray

cd tester_bug_v2ray

curl -L -o v2ray.zip https://github.com/v2fly/v2ray-core/releases/latest/download/v2ray-linux-arm64-v8a.zip

unzip -o v2ray.zip v2ray

chmod +x v2ray

ketik micro config.json edit dan tmbahkan akun dan bug disana

{
  "vmess": "vmess://AKUN VMESS ANDA",
  "bugs": [
    "arjuna.bug",
    "apac-market.bug",
    "TAMBAHKAN BUG LAGI",
  ],
  "local_port": 10808,
  "timeout": 15,
  "stop_on_success": false,
  "tests": [
    "address",
    "ws_host",
    "sni"
  ],
  "fingerprint": "chrome",
  "allowInsecure": true,
  "test_url": "https://www.cloudflare.com/cdn-cgi/trace"
}

UNTUK SAVE TEKAN 'ctrl+q' lalu 'y'

## 📦 Menjalankan script
python v2ray.py

cek hasil penuh di response.json.


NOTE : JIKA TEST BUG JANGAN GUNAKAN VPN ATAUPUN KUOTA UTAMA.  SESUAIKAN DENGAN BUG JIKA OPOK GUNAKAN KARTU OPOK, JIKA SAWER GUNAKAN KUOTA SAWER.
