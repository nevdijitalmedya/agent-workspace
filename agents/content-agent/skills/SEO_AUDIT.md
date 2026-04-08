# Skill: SEO Audit

## Purpose

Yayınlanmış makalelerin GEO/SEO uyumunu denetlemek, eksikleri raporlamak ve öğrenimleri MEMORY.md'ye yazmak.

## Serves Goal

Organik trafik, GEO görünürlüğü

## Trigger

- Yayından 7 gün geçmiş makale var
- Haftalık review döngüsü

## Inputs

| Source | What to read |
| --- | --- |
| `outputs/YYYY-MM-DD_publish-log.md` | Yayınlanan makale listesi |
| `outputs/YYYY-MM-DD_draft_[slug].md` | Orijinal taslak |
| `knowledge/STRATEGY.md` | Hedef metrikler |

## Process

1. Yayın loglarından son 30 günde yayınlananları listele
2. Her makale için denetim yap:

### Denetim Kriterleri

| Kriter | Kontrol | Hedef |
| --- | --- | --- |
| Title uzunluğu | 50-60 karakter arası mı? | Evet |
| Meta description | 120-155 karakter, anahtar kelime var mı? | Evet |
| H1 başlık | Anahtar kelime içeriyor mu? | Evet |
| İç linkleme | En az 1 iç link var mı? | Evet |
| GEO yapısı | Soru formatı H2'ler var mı? | Evet |
| Schema markup | FAQ veya HowTo schema var mı? | Tercih edilir |
| Kelime sayısı | 600+ kelime mi? | Evet |

3. Eksikleri listele
4. Düzeltilmesi gerekenleri `outputs/YYYY-MM-DD_seo-audit.md` olarak yaz
5. Tekrar eden eksikleri MEMORY.md'ye yaz (pattern öğrenimi)
6. Journal'a özet yaz

## Output

`outputs/YYYY-MM-DD_seo-audit.md`

## Audit Report Format

```markdown
# SEO Denetim Raporu — YYYY-MM-DD

## Denetlenen Makaleler

| Başlık | URL | Puan | Eksikler |
| --- | --- | --- | --- |
| [başlık] | [url] | 7/8 | Schema yok |

## Kritik Eksikler

- [Makale]: [Eksik] — Önerilen düzeltme: ...

## Öğrenimler (MEMORY.md'ye eklenecek)

- ...
```

## Rules

- Düzeltmeleri doğrudan WordPress'te uygulama — raporu insana sun
- Aynı eksikliği her denetimde tekrar yazma — pattern olarak MEMORY.md'ye kaydet
- Denetim olmayan haftaları journal'a kaydet
