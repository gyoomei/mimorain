# 🌧️ MiMoRain

### Curah Hujan Real-Time — Powered by Xiaomi MiMo V2.5

Dashboard curah hujan real-time yang mengambil data dari Open-Meteo API (gratis, tanpa API key). Pantau presipitasi saat ini, grafik 24 jam, prakiraan 7 hari, dan insight cuaca dari MiMo. Animasi hujan Canvas yang responsif terhadap intensitas hujan. Zero dependencies, single HTML file.

[![Live Demo](https://img.shields.io/badge/Live-Demo-000?style=for-the-badge&logo=github)](https://gyoomei.github.io/mimorain/)
[![Try Now](https://img.shields.io/badge/Try-Now-3b82f6?style=for-the-badge&logo=googlechrome)](https://gyoomei.github.io/mimorain/)
[![AI](https://img.shields.io/badge/AI-Xiaomi%20MiMo%20V2.5-f97316?style=for-the-badge)](https://mimo.xiaomi.com/)
[![API](https://img.shields.io/badge/API-Open--Meteo-22c55e?style=for-the-badge)](https://open-meteo.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## 📖 The Problem

Apps cuaca umum (BMKG, AccuWeather, Google Weather) menampilkan data dalam format tabel atau ikon statis. Tidak ada visualisasi curah hujan yang intuitif — grafik per jam, animasi hujan real-time, atau insight AI yang menjelaskan "apakah saya butuh payung hari ini?" — yang bisa diakses tanpa install aplikasi.

## ✨ How it works

```
You type:     "Jakarta" atau klik 📍 Lokasi Saya
You see:      Curah hujan saat ini + grafik 24 jam + prakiraan 7 hari
You watch:    Canvas rain animation berubah sesuai intensitas
You read:     MiMo insight: "Hujan lebat, hindari area rawan banjir"
```

**That's the entire UX** — cari kota, lihat data, baca insight. Tidak perlu install, tidak perlu API key.

## 🎯 Core Features

| Capability | Detail |
|---|---|
| Data Source | Open-Meteo API — free, no key, CORS `*`, global coverage |
| Current Weather | Curah hujan (mm/jam), probabilitas, showers, elevasi |
| 24-Hour Chart | Bar chart presipitasi + line chart probabilitas per jam |
| 7-Day Forecast | Grid kartu per hari dengan total mm + probabilitas |
| Rain Animation | Canvas particle drops yang responsif terhadap intensitas hujan |
| AI Insight | Analisis kondisi: "Cerah", "Siapkan payung", "Waspada banjir" |
| City Search | 25+ kota built-in + geocoding global via Open-Meteo |
| Geolocation | 📍 tombol untuk auto-detect lokasi pengguna |
| Dark/Light Theme | Toggle dengan persistence |
| Mobile Responsive | Grid adaptif, search bar wrap |

## 🏗️ Architecture

```
┌──────────────────────────────────────────────┐
│  Open-Meteo API (free, no key)               │
│  /v1/forecast?hourly=precipitation,rain,...   │
│       │                                       │
│  ┌────┴──────────────────────────────────┐   │
│  │ Current Card  │  24h Chart  │ 7-Day   │   │
│  │ (mm/jam,      │  (Canvas    │ Grid    │   │
│  │  prob, icon)  │   bars +    │ Cards)  │   │
│  │               │   prob line)│         │   │
│  └────┬──────────┴─────────────┴─────────┘   │
│       │                                       │
│  Canvas Rain Animation                        │
│  (particle drops, splash, intensity-reactive) │
│       │                                       │
│  MiMo Insight                                 │
│  (rule-based: cerah/gerimis/lebat/banjir)     │
└──────────────────────────────────────────────┘
```

## 💡 Architecture Decisions

**Why Open-Meteo?** Free, no API key, global coverage, CORS enabled, Indonesian timezone support. Returns precipitation, rain, showers, and probability per hour for 7 days. No rate limit for reasonable use.

**Why rule-based insight?** MiMo 100T projects use Pollinations.ai for AI chat, but weather insight needs instant response. Simple rules (rain > 10mm = "banjir", prob > 60% = "bawa payung") give faster, more reliable answers than waiting for LLM response.

**Why Canvas rain animation?** A static chart shows data; animated rain drops show the *feeling* of the weather. Intensity directly controls drop count, speed, and opacity — heavy rain has 300 fast drops, light drizzle has 50 slow ones.

## 🧪 Try these examples

| City | What to expect |
|---|---|
| Jakarta | Tropical rain — frequent afternoon showers, high humidity |
| Surabaya | Similar to Jakarta, slightly drier |
| Denpasar | Bali weather — seasonal patterns |
| Tokyo | Temperate — more variable rainfall |
| London | Famous for drizzle — expect low-moderate precipitation |

## 🛠️ Stack

- **Frontend:** Vanilla JavaScript, single HTML file (~26KB)
- **API:** [Open-Meteo](https://open-meteo.com/) — free weather API, no key required
- **Rendering:** Canvas 2D for chart + rain animation
- **Fonts:** [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) + [Outfit](https://fonts.google.com/specimen/Outfit) + [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)
- **Hosting:** GitHub Pages (zero infra cost)

## 🚀 Quick Start

```bash
git clone https://github.com/gyoomei/mimorain.git
open mimorain/index.html
# or
python3 -m http.server 8080 -d mimorain
```

## 📄 License

MIT — free for personal and commercial use.

**Built with 🧠 [Xiaomi MiMo V2.5](https://mimo.xiaomi.com/) · Submitted to [MiMo 100T program](https://mimo.xiaomi.com/)**
