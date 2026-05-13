# 🚀 DeployCC --- Deployment Guide

!!!!! DIWAJIBKAN UNTUK GANTIAN MENDEPLOY
jika error segera hubungi asdos

------------------------------------------------------------------------

## 🧩 1. Setup GitHub Actions CD

Salin file berikut ke repository:

``` bash
.github/workflows/cd.yml
```

Workflow ini adalah **CD --- Deploy ke DeployCCC** yang berjalan
otomatis.

------------------------------------------------------------------------

## 🔄 2. Auto Deploy dari CI

Deploy akan berjalan otomatis jika:

-   ✅ CI Pipeline sukses
-   🔁 atau manual trigger (`workflow_dispatch`)

------------------------------------------------------------------------

## 🚀 3. Full Deployment (First Push)

Saat push pertama, sistem akan otomatis:

-   ⚡ Build frontend (React/Vite)
-   🐍 Setup backend Python
-   ⚙️ Generate `.env`
-   🗄 Auto-create PostgreSQL database
-   🌐 Deploy Nginx + Cloudflared tunnel
-   🚀 Run Uvicorn service

------------------------------------------------------------------------

## 🌐 4. Install Cloudflared & SSH

### Windows

``` bash
cloudflared.bat
ssh.bat
```

### macOS / Linux

``` bash
brew install cloudflared (via terminal)
./ssh.sh
```

------------------------------------------------------------------------

## 🔐 5. SSH Login

Credential SSH akan muncul di:

> GitHub Actions → DeployCC Summary

------------------------------------------------------------------------

## 🐍 6. Setup Backend Environment

``` bash
python3.12 -m venv venv --clear

venv/bin/pip install --upgrade pip
venv/bin/pip install -r backend/requirements.txt
venv/bin/pip install uvicorn[standard]
```

------------------------------------------------------------------------

## 🗄 7. Database Setup (dbtool)

Login ke server menggunakan ssh.bat/sh:

``` bash
ssh dbtool@server
# password: cc
```

Lalu buat database:

``` sql
CREATE DATABASE nama_db;
```

------------------------------------------------------------------------

## ▶️ 8. Run Backend Manual

``` bash
python -m uvicorn main:app --host 127.0.0.1 --port xxxx (untuk port terdapat di github action)
```

------------------------------------------------------------------------

## ⚙️ Service Control

``` bash
systemctl status deploycc-<repo>.service
systemctl restart deploycc-<repo>.service
```

------------------------------------------------------------------------

## 🧪 Troubleshooting Uvicorn

Jika error:

``` bash
source venv/bin/activate
python -m uvicorn main:app --host 127.0.0.1 --port xxxx
```

Pastikan muncul:

    🔐 CORS Allowed Origins: ['https://xxxxxx.akhzafachrozy.my.id']
    ✅ CORS middleware configured successfully

------------------------------------------------------------------------

## 🎯 Done

Jika semua berhasil:

-   🌍 Web sudah live
-   🐍 Backend aktif
-   🗄 Database connected
-   ☁ Cloudflared tunnel running
#
