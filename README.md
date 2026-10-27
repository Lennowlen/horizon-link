# HorizonLink — Open Nintendo Switch CFW Online Network & Infrastructure

HorizonLink adalah infrastruktur jaringan online mandiri (*open-source online network & matchmaking stack*) untuk konsol Nintendo Switch Custom Firmware (Atmosphere CFW) dan emulator (Ryujinx).

Proyek ini dibangun untuk komunitas gaming, memungkinkan pemain untuk mabar (*multiplayer online*) secara aman tanpa risiko ban dari server resmi Nintendo, dengan akun, profil, friend code mandiri, serta integrasi pemantauan server dan donasi komunitas.

---

## 🌟 Fitur & Keunggulan HorizonLink
1. **Plug & Play MicroSD Setup**:
   - Generator otomatis file konfigurasi `sdmc:/atmosphere/hosts/emummc.txt` (DNS.mitm) dan homebrew client `HorizonLink.nro`. Cukup drag-and-drop ke microSD tanpa perlu utak-atik manual.
2. **Built-in Nginx Conntest & Telemetry Sink**:
   - Menghilangkan masalah popup *"Wi-Fi Login Required"* pada koneksi Switch dan mencegah applet NSO freeze saat membuka profil dengan proxy dummy HTTP 200 `X-Organization: Nintendo`.
3. **Live Server Monitoring & Web Portal**:
   - Web Portal modern bernuansa Dark-mode clean (Tailwind & responsive) untuk pendaftaran akun, Friend Code generator, status room matchmaking game (Mario Kart 8 DX, Smash Ultimate, Splatoon 2), serta **Dukungan Donasi Komunitas (Trakteer Zeyrann)** untuk biaya operasional server.
4. **Cloud CI/CD Otomatis (GitHub Actions)**:
   - **Auto-Deploy Server VPS** (`.github/workflows/deploy-server.yml`): Push ke branch `main` langsung otomatis deploy stack Docker Compose ke VPS rann-labs via SSH.
   - **Auto-Build Switch Client** (`.github/workflows/build-switch-client.yml`): Runner cloud menggunakan container `devkitpro/devkita64` untuk compile `HorizonLink.nro` dari kode C dan mengemas artefak rilis `HorizonLink-Switch-SDCard.zip`.

---

## 🏗️ Komponen Arsitektur Stack Server
- `sni-router`: Port 443 TLS SNI passthrough router.
- `horizonlink-account`: Port 8080 REST API user, friend code, presence, dan token authentication.
- `horizonlink-nex`: Engine matchmaking dan protokol reliabel UDP (NEX / PRUDP) untuk Mario Kart 8 Deluxe (:60003), Super Smash Bros Ultimate (:60005), dan Splatoon 2 (:60004).
- `horizonlink-nncs`: NAT-check responder untuk koneksi P2P Pia.
- `nginx-gateway`: Port 80 conntest & telemetri sink.
- `web-portal`: Port 3000 Web UI portal komunitas.

---

## ⚙️ GitHub Secrets yang Dibutuhkan untuk Deploy:
Tambahkan nilai-nilai berikut di menu **Settings -> Secrets and variables -> Actions** di repositori ini:

| Nama Secret | Keterangan |
| --- | --- |
| `RANN_LABS_HOST` | IP publik atau domain VPS rann-labs |
| `RANN_LABS_USER` | Username SSH VPS (misal: `root` atau `ubuntu`) |
| `RANN_LABS_SSH_KEY` | Private SSH Key untuk login ke VPS |
| `RANN_LABS_PORT` | Port SSH (default: 22) |
| `RANN_LABS_SERVER_IP` | IP publik utama server |
| `RANN_LABS_NAT_IP` | IP publik kedua untuk dual vantage point NAT-check (opsional) |
| `HORIZONLINK_BASE_URL` | URL publik web portal (misal: `https://horizon.rann-labs.com`) |
| `NEXTENDO_SECRET` | 32 karakter acak hex untuk JWT token signing |
| `NEXTENDO_INTERNAL_KEY` | Secret komunikasi antar-service internal |
| `NEXTENDO_SECURE_PASSWORD` | Password secure auth server |

---

## ☕ Dukungan & Donasi Komunitas
Infrastruktur dan server HorizonLink dikelola secara swadaya untuk komunitas game Switch CFW. Anda dapat mendukung kelangsungan hosting dan pengembangan fitur baru melalui [Trakteer Zeyrann](https://trakteer.id/zeyrann).
