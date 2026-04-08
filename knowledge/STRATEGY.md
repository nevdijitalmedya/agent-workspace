# Strategy

## Current Priorities

1. İçerik otomasyonu: n8n ile AI üretimi içerikleri WordPress'e otomatik basmak
2. GEO/SEO: Headless WP + Astro mimarisiyle organik görünürlüğü artırmak
3. Blog büyütme: Düzenli, segmente özel teknik içeriklerle otorite inşa etmek

## This Quarter's Goals

| Goal | Metric | Current | Target |
| --- | --- | --- | --- |
| Blog trafiği | Aylık organik ziyaretçi | — | +%50 |
| İçerik hacmi | Yayınlanan makale/ay | 0 | 8+ |
| GEO görünürlüğü | AI botlarından gelen referans | — | Ölçülebilir varlık |
| Sayfa hızı | Core Web Vitals (LCP) | — | <1.5s (Astro/Vercel) |

## Architecture

- **Backend:** WordPress (Güzel Hosting) — Headless CMS, sadece API
- **Frontend:** Astro (Vercel) — `/blog` rotası WP REST API'den veri çeker
- **Otomasyon:** n8n (VPS/Coolify) — AI içerik üretip WP'ye REST API ile basar

## Not Doing (Deliberately)

- WordPress tema/arayüz geliştirmesi yok (ziyaretçi görmeyecek)
- Sosyal medya dağıtımı şimdilik kapsam dışı (ayrı agent)
- Ücretli reklam kampanyası kapsam dışı
