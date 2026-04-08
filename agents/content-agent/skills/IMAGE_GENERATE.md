# Skill: Image Generate

## Purpose

Makale içeriğine uygun, SEO-friendly görsel üretmek. Gemini Imagen 2 API kullanır. Üretilen görseli WordPress media library'ye yükler ve makaleye featured image olarak atar.

## Serves Goal

GEO görünürlüğü, İçerik kalitesi

## Trigger

CONTENT_GENERATE skill'i taslak oluşturduktan hemen sonra çalışır.

## Inputs

| Source | What to read |
| --- | --- |
| `outputs/YYYY-MM-DD_draft_[slug].md` | Makale başlığı, anahtar kelime, segment |
| `knowledge/BRAND.md` | Marka renk/stil rehberi |

## Process

1. Taslak dosyasından şunları oku: `title`, `target_keyword`, `segment`
2. Prompt oluştur (aşağıdaki formata göre)
3. Gemini Imagen 2 API'ye istek at
4. Dönen base64 görselini decode et
5. WordPress media library'ye yükle (multipart/form-data)
6. Dönen `media_id`'yi taslak dosyasının front matter'ına yaz: `featured_image_id`

## Imagen 2 API Call

```bash
curl -s -X POST \
  "https://generativelanguage.googleapis.com/v1beta/models/imagen-2.0-generate-001:predict?key=${GEMINI_API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "instances": [{"prompt": "PROMPT_HERE"}],
    "parameters": {
      "sampleCount": 1,
      "aspectRatio": "16:9",
      "safetyFilterLevel": "block_some"
    }
  }'
```

## Prompt Şablonu

```
Professional, clean illustration for a B2B technical article.
Topic: [target_keyword]
Industry: [segment — industrial / medical / architectural / advertising]
Style: Modern, minimalist, corporate. No text or watermarks.
Mood: Professional, trustworthy, innovative.
Color palette: Deep navy blue, white, subtle silver accents.
```

Segment'e göre ek stil:
- **endüstriyel:** "Technical machinery, engineering components, precision manufacturing"
- **medikal:** "Clean medical environment, scientific visualization, human anatomy (tasteful)"
- **mimari:** "Architectural rendering, modern building, clean lines"
- **reklam:** "Creative studio, 3D rendering workspace, digital art"

## WordPress Media Upload

```bash
# Görseli yükle
curl -s -X POST \
  "https://nevdijital.com/blog/wp-json/wp/v2/media" \
  -H "Authorization: Basic BASE64(username:app_password)" \
  -H "Content-Disposition: attachment; filename=SLUG-featured.jpg" \
  -H "Content-Type: image/jpeg" \
  --data-binary @/tmp/generated-image.jpg
```

Dönen JSON'dan `id` alanını al → taslak front matter'a `featured_image_id: [id]` olarak ekle.

## Output

Taslak dosyasına eklenen satırlar:

```markdown
featured_image_id: 123
featured_image_url: https://nevdijital.com/blog/wp-content/uploads/...
image_prompt: [kullanılan prompt]
```

## Error Handling

- Imagen API 429 (rate limit): 60 saniye bekle, tekrar dene
- Imagen API hatası: Görselsiz devam et, taslağa `featured_image_id: none` yaz, journal'a logla
- WP media upload hatası: Görsel dosyasını `outputs/images/` klasörüne kaydet, insana bildir

## Rules

- Her makale için 1 görsel üret (fazlası değil)
- Görsel promptunda marka adı, insan yüzü veya telif hakkı içerebilecek unsurlar kullanma
- Yüklenen görseli `outputs/images/YYYY-MM-DD_[slug].jpg` olarak da kaydet (yedek)
- `featured_image_id: none` olan taslaklar WP_PUBLISH'te görselsiz yayınlanır
