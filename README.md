# Showcar – PWA 360 (Feria virtual de autos)

Feria virtual **multi-marca** con **vistas 360° reales** (Photo-Sphere-Viewer), instalable como **PWA**, enfocada en **leads** por dealer.

> Este README define el plan técnico, cómo correr el proyecto y las convenciones.  
> Estado del MVP: **scaffold pendiente** (lo generará Codex a partir de este plan).

---

## 🧭 Objetivo

Crear un **repo base** con:
- **Vite + React + TypeScript + Tailwind + vite-plugin-pwa**
- **Photo-Sphere-Viewer** (demo de panorámica 360 con *blur-up*)
- **Rutas base**: `/`, `/brand/:id`, `/model/:id`, `/model/:id/360`
- Calidad: **ESLint + Prettier + Husky + lint-staged + TS strict**
- Pruebas: **Vitest + Testing Library**, **Playwright (smoke)**
- **GitHub Actions**: lint, test, build
- **Deploy**: Cloudflare Pages (o Vercel)

---

## 🧱 Stack

- **App**: Vite, React, TypeScript, React Router, TailwindCSS
- **PWA**: vite-plugin-pwa + Workbox (SW + manifest)
- **360**: Photo-Sphere-Viewer
- **Estado**: React Query (datos) + Zustand (UI ligera) *(post-scaffold)*
- **Calidad**: ESLint, Prettier, Husky, lint-staged, TS strict
- **Tests**: Vitest, Testing Library, Playwright (smoke)
- **CI/CD**: GitHub Actions
- **Hosting**: Cloudflare Pages (recomendado) o Vercel Hobby

---

## ✅ Requisitos funcionales (MVP)

- **Rutas**
  - `/` Home (grid de marcas)
  - `/brand/:id` Modelos de la marca
  - `/model/:id` Ficha del modelo (+ CTA lead)
  - `/model/:id/360` Visor 360
- **Componentes**
  - `BrandGrid`, `ModelCard`, `PanoViewer`, `LeadModal`, `OrientationOverlay`
- **PWA**
  - Manifest con íconos **192/512**, `display: standalone|fullscreen`, preferencia **landscape**
- **Service Worker (estrategias)**
  - HTML: `NetworkFirst` + fallback **offline**
  - Estáticos: `CacheFirst` (versionado)
  - **Panoramas**: `CacheFirst` con **LRU** (`maxEntries: 30`, `maxAge: 30d`)
- **Assets 360**
  - Convención: `/public/panoramas/{brand}/{model}/`
  - Dos tamaños: `*_4096.webp` (móvil) y `*_6144.webp` (desktop)  
    *(opcional AVIF: `*_4096.avif`, `*_6144.avif`)*
  - Preview borroso: `*_preview_256.jpg` (10–20 KB)
- **PanoViewer**
  - FOV 65–75, zoom limitado, *blur-up* mientras carga
- **Leads**
  - WhatsApp **deeplink** + formulario (stub con Supabase opcional)
  - Envs: `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`
- **Analytics (GA4)**
  - Eventos: `pwa_install`, `pano_open`, `pano_dwell_time`, `lead_submit`, `wa_click`

---

## 🎯 Criterios de aceptación

- `npm run dev` compila sin errores
- Lighthouse (home) **PWA/Best Practices ≥ 90**
- Visor 360 carga una **demo** con *blur-up*
- SW cachea panoramas con **LRU**
- Lead mock muestra **success/failure**
- CI ejecuta **lint/test/build** en PRs

---

## 🧩 Estructura esperada (tras el scaffold)

