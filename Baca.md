# 🧠 WormGPT Bot Setup Guide

WormGPT Bot adalah proyek berbasis **Node.js** yang terhubung dengan **OpenRouter API** dan **Telegram Bot API**.  
Bot ini bisa dijalankan secara lokal (terminal), di **VSCode**, maupun di server dengan **Pterodactyl Panel**.

---

## ⚙️ 1. Persiapan Awal

### ✅ Pastikan Lo Punya
- Node.js v18 atau lebih baru  
- npm (biasanya udah otomatis ikut Node.js)
- File `config.json` (isi API key, token Telegram, dll)
- Akses ke terminal (cmd, bash, atau panel console)

---

## 📦 2. Ekstrak File Project

Kalau file-nya masih `.tar.gz`, ekstrak dulu:

```bash
tar -xvzf fileworm.tar.gz
cd fileworm
```

> Pastikan di dalam folder itu ada file seperti:
> ```
> wormgpt_bot.js
> package.json
> config.json
> ```

---

## 🧰 3. Instal Dependensi

Jalankan:
```bash
npm install
```

Kalau ada error permission, coba:
```bash
npm install --force
```

---

## 🧪 4. Konfigurasi `config.json`

Edit file `config.json` pakai text editor / VSCode:

```bash
nano config.json
```

Isi data penting kayak:
```json
{
  "openrouter_api_key": "sk-or-v1-xxxx",
  "telegram_token": "1234567890:AAAxXXXX",
  "owner_id": 1234567890,
  "base_url": "https://openrouter.ai/api/v1",
  "model": "deepseek/deepseek-chat",
  "language": "Indonesia",
  "free_limit": 5,
  "site_url": "https://example.com",
  "site_name": "WormGPT AryzXPloit",
  "required_channel": "@Aryzzstores"
}
```

> ⚠️ Jangan pernah upload file ini ke GitHub publik, karena ada API key & token sensitif.

---

## 💻 5. Cara Jalanin di Terminal (Manual)

```bash
node wormgpt_bot.js
```

Kalau mau jalan terus walau terminal ditutup, bisa pake:
```bash
npm install -g pm2
pm2 start wormgpt_bot.js --name wormgpt
pm2 logs wormgpt
```

Cek status:
```bash
pm2 list
```

---

## 🧩 6. Cara Jalanin di VSCode

1. Buka folder project lo di VSCode  
2. Pastikan `config.json` udah diisi  
3. Di terminal VSCode:
   ```bash
   npm install
   node wormgpt_bot.js
   ```
4. Kalau mau pakai **debug mode**, buat file `.vscode/launch.json`:
   ```json
   {
     "version": "0.2.0",
     "configurations": [
       {
         "type": "node",
         "request": "launch",
         "name": "Run WormGPT Bot",
         "skipFiles": ["<node_internals>/**"],
         "program": "${workspaceFolder}/wormgpt_bot.js"
       }
     ]
   }
   ```
5. Klik tombol **Run ▶️ (F5)** buat jalanin langsung dari VSCode.

---

## 🚀 7. Deploy di Panel Pterodactyl

### 🔧 Upload File
1. Upload hasil ekstrak (`wormgpt_bot.js`, `package.json`, `config.json`) ke server lo lewat File Manager Pterodactyl.
2. Atau upload file `.tar.gz` dan ekstrak lewat console:
   ```bash
   tar -xvzf fileworm.tar.gz
   ```

### 🔨 Install Dependensi
Masuk console panel:
```bash
npm install
```

### ⚡ Jalankan Bot
Jalanin bot di console panel:
```bash
node wormgpt_bot.js
```

Kalau mau auto restart pas bot crash:
```bash
npm install -g pm2
pm2 start wormgpt_bot.js --name wormgpt
```

### 🧱 (Opsional) Auto-start saat server nyala
Tambahkan command ke startup field di panel:
```
node wormgpt_bot.js
```
Atau pakai script `start.sh` kayak gini:
```bash
#!/bin/bash
npm install
node wormgpt_bot.js
```

---

## 🔍 8. Tes Token & API Key

### Cek Token Telegram
```bash
curl https://api.telegram.org/bot<YOUR_TOKEN>/getMe
```

### Cek OpenRouter API Key
```bash
curl https://openrouter.ai/api/v1/models -H "Authorization: Bearer sk-or-v1-xxxx"
```

Kalau dua-duanya balik response JSON yang valid → berarti config lo udah benar 🎯

---

## 🛠️ 9. Tips & Troubleshooting

| Masalah | Solusi |
|----------|---------|
| Bot gak respon | Cek `telegram_token` & `owner_id` |
| Error “Cannot find module” | Jalankan `npm install` lagi |
| Token invalid | Cek di [@BotFather](https://t.me/BotFather) |
| Port blocked (di panel) | Ganti mode ke polling, bukan webhook |
| Crash tiba-tiba | Gunakan `pm2 logs wormgpt` untuk lihat error |

---

## 🧤 10. Keamanan

- Jangan bagikan file `config.json` ke publik  
- Simpan key di `.env` kalau di production  
- Pakai `chmod 600 config.json` biar file gak bisa dibaca orang lain di server  
- Rutin rotate API key tiap beberapa bulan  

---

## 📞 Support

Kalau butuh bantuan setup, update script, atau error log, bisa hubungi:
- Telegram: [@Aryzzstores](https://t.me/Aryzzstores)
- Website: [https://panel.aryapanel.xyz](https://panel.aryapanel.xyz)
