# Nextendo Rann-Labs Private Server & Switch Client

Repositori monorepo terpadu untuk backend server game Nintendo Switch CFW dan otomatisasi build client Atmosphere berbasis GitHub Actions.

## Fitur & Komponen
1. **Auto-Deploy ke VPS Rann-Labs** (`.github/workflows/deploy-server.yml`):
   - Otomatis deploy stack Docker Compose (`sni-router`, `nextendo-account`, `nextendo-nex`, `nextendo-nncs`, `nginx-gateway`, dan `web-portal`) via SSH Action setiap push ke branch `main`.
2. **Auto-Build Switch Client & SD Card Package** (`.github/workflows/build-switch-client.yml`):
   - Menggunakan image resmi `devkitpro/devkita64` untuk mengompilasi `Prelude.nro` dengan injeksi host/IP server rann-labs.
   - Otomatis merakit file ZIP SD Card plug-and-play (`atmosphere/hosts/emummc.txt` & `switch/Prelude-RannLabs.nro`).
3. **Web Portal Baru**:
   - Frontend modern (Dark theme clean) untuk registrasi akun pemain, generator Friend Code, dan live server monitoring.

## GitHub Secrets yang Perlu Dikonfigurasi di Repository:
- `RANN_LABS_HOST`: IP publik VPS rann-labs
- `RANN_LABS_USER`: Username SSH VPS (misal: `root` atau `ubuntu`)
- `RANN_LABS_SSH_KEY`: Private SSH Key untuk login ke VPS
- `RANN_LABS_SERVER_IP`: IP Publik utama server (untuk game auth, nex, web)
- `RANN_LABS_NAT_IP`: IP Publik kedua (opsional, jika ada 2 IP untuk dual vantage point NAT-check)
- `NEXTENDO_BASE_URL`: URL Portal (misal: `https://switch.rann-labs.com`)
- `NEXTENDO_SECRET`: Secret 32 karakter hex untuk token signing
- `NEXTENDO_INTERNAL_KEY`: Secret internal service auth
- `NEXTENDO_SECURE_PASSWORD`: Password secure internal
