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
chmod +x ssh.sh
./ssh.sh
```

------------------------------------------------------------------------

## 🔐 5. SSH Login

Credential SSH akan muncul di:

> GitHub Actions → DeployCC Summary

------------------------------------------------------------------------

## 🐍 6. Setup Backend Environment 

difolder repostory bukan backend/frontend

``` bash
# masuk ke folder project
ssh sudah otomatis didalam folder project

# (opsional) hapus venv lama kalau rusak
rm -rf venv

# buat venv baru
python3 -m venv venv

# aktifkan venv
source venv/bin/activate

# upgrade pip
pip install --upgrade pip

# install dependencies project
pip install -r backend/requirements.txt

# install uvicorn + dependencies lengkap
pip install "uvicorn[standard]"
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
