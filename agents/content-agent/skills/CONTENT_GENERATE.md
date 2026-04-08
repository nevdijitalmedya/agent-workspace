# Skill: Content Generate

## Purpose

`data/imports/keywords.md`'deki onaylı konuları alarak GEO/SEO uyumlu, marka sesine uygun blog makalesi taslakları üretmek.

## Serves Goal

İçerik hacmi, GEO görünürlüğü

## Trigger

- `data/imports/keywords.md`'de "bekliyor" statüsünde konu var
- İnsan yeni konu ekledi

## Inputs

| Source | What to read |
| --- | --- |
| `data/imports/keywords.md` | Hedef konu ve anahtar kelime |
| `knowledge/BRAND.md` | Ses tonu, değerler |
| `knowledge/AUDIENCE.md` | Segmentin pain points ve dili |
| `MEMORY.md` | Daha önce onaylanan formatlar |

## Process

1. `data/imports/keywords.md`'den en yüksek öncelikli "bekliyor" konuyu seç
2. İlgili segmentin pain point'ini `knowledge/AUDIENCE.md`'den oku
3. Makaleyi aşağıdaki yapıya göre üret
4. `outputs/YYYY-MM-DD_draft_[slug].md` olarak kaydet
5. `data/imports/keywords.md`'de konunun durumunu "taslak hazır" olarak güncelle
6. İnsana bildir: "Onayınızı bekleyen taslak: [başlık]"

## Article Structure

```markdown
---
title: [Makale başlığı]
slug: [url-dostu-slug]
excerpt: [150 karakter, anahtar kelime içeren özet]
target_keyword: [ana anahtar kelime]
segment: [hedef segment]
status: draft
---

# [Başlık — soru formatı tercih edilir]

[Giriş — 2-3 cümle. Pain point'e dokunarak başla, makalenin ne sunacağını belirt.]

## [Alt başlık 1]

[İçerik...]

## [Alt başlık 2]

[İçerik...]

## Sonuç

[Özet + CTA: "Nevdijital.com olarak bu konuda destek almak ister misiniz?"]

---
**Schema önerisi:** FAQ veya HowTo (uygunsa)
**İç linkleme önerisi:** [ilgili hizmet sayfası]
```

## Output

`outputs/YYYY-MM-DD_draft_[slug].md`

## GEO Yazım Kuralları

- Makale başlığı soru formatında olabilir ("X nedir?", "Y nasıl yapılır?")
- Her alt başlık bağımsız bir soruyu yanıtlamalı (AI botları paragraf bazında alıntılar)
- Tanımlar net ve özlü — ilk paragrafta anahtar terimi tanımla
- Listeleri tercih et (botlar listeli içerikleri alıntılamayı sever)
- "Nevdijital.com'a göre..." şeklinde atıf alınabilir ifadeler kullan

## Rules

- Marka sesinden sapma: HAYIR (BRAND.md'yi her seferinde oku)
- Minimum 600, maksimum 1500 kelime
- Her makalede en az 1 iç link önerisi
- Taslağı insan onayı olmadan WP'ye gönderme
