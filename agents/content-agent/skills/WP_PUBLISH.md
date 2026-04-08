# Skill: WP Publish

## Purpose

İnsan tarafından onaylanmış taslakları WordPress REST API aracılığıyla yayınlamak ve yayın logunu kaydetmek.

## Serves Goal

İçerik hacmi

## Trigger

- İnsan bir taslağı "onaylandı" olarak işaretledi
- `outputs/` klasöründe `status: approved` olan taslak var

## Inputs

| Source | What to read |
| --- | --- |
| `outputs/YYYY-MM-DD_draft_[slug].md` | Onaylı taslak içeriği |
| `MEMORY.md` | WordPress API endpoint bilgileri |

## Process

1. Onaylı taslağı `outputs/` klasöründen oku
2. Front matter'dan title, slug, excerpt, content'i parse et
3. WordPress REST API'ye POST at:

```
POST https://nevdijital.com/blog/wp-json/wp/v2/posts
Authorization: Bearer [WP_APP_PASSWORD]
Content-Type: application/json

{
  "title": "[başlık]",
  "slug": "[slug]",
  "excerpt": "[özet]",
  "content": "[makale içeriği — HTML]",
  "status": "publish",
  "categories": [...],
  "meta": {
    "rank_math_focus_keyword": "[anahtar kelime]"
  }
}
```

4. API'den dönen post URL'ini al
5. Yayın logu oluştur: `outputs/YYYY-MM-DD_publish-log.md`
6. Journal'a yaz: yayın tarihi, başlık, URL
7. Taslak dosyasında `status: published` olarak güncelle

## Output

- WordPress'te yayınlanmış makale
- `outputs/YYYY-MM-DD_publish-log.md`
- `journal/entries/YYYY-MM-DD_HHMM.md` girişi

## Publish Log Format

```markdown
# Yayın Logu — YYYY-MM-DD

| Alan | Değer |
| --- | --- |
| Başlık | [başlık] |
| Slug | [slug] |
| URL | https://nevdijital.com/blog/[slug] |
| Yayın tarihi | YYYY-MM-DD HH:MM |
| Anahtar kelime | [keyword] |
| Segment | [segment] |
| Durum | Yayınlandı |
```

## Error Handling

- API 401 döndürürse: İnsana bildir — uygulama şifresi süresi dolmuş olabilir
- API 422 döndürürse: Slug çakışması — slug'a tarih ekle ve tekrar dene
- Bağlantı hatası: Journal'a yaz, insan'a eskal et

## Rules

- `status: approved` olmayan taslağı asla yayınlama
- Aynı slug'ı iki kez gönderme (MEMORY.md'deki yayın logunu kontrol et)
- Her yayın journal'a kayıt edilmeli
