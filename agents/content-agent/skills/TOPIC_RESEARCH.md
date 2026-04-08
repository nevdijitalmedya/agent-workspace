# Skill: Topic Research

## Purpose

Nevdijital.com için GEO/SEO değeri yüksek, hedef kitleye uygun blog konuları araştırmak ve önceliklendirmek.

## Serves Goal

İçerik hacmi, Organik trafik

## Trigger

- `data/imports/keywords.md` boş veya güncellenmediyse
- Pipeline'da yayınlanacak taslak kalmadıysa

## Inputs

| Source | What to read |
| --- | --- |
| `knowledge/AUDIENCE.md` | Segmentler ve pain points |
| `knowledge/STRATEGY.md` | Mevcut öncelikler |
| `MEMORY.md` | Geçmişte iyi çalışan konu kategorileri |
| `journal/entries/` | Son döngülerde neler üretildi |

## Process

1. `knowledge/AUDIENCE.md`'den 4 segmenti oku
2. Her segment için 3 pain point belirle
3. Her pain point için şu format ile konu üret:
   - **Başlık:** "Soru formatı veya Nasıl/Ne/Neden"
   - **Anahtar kelime:** Ana hedef kelime
   - **Segment:** Hangi kitleye hitap ediyor
   - **GEO notu:** AI botlarının bu konuyu alıntılama ihtimali (yüksek/orta/düşük)
   - **Öncelik:** 1–5 arası
4. Listede zaten yayınlanmış konularla çakışma var mı kontrol et (`outputs/` klasöründen)
5. En yüksek öncelikli 5 konuyu `data/imports/keywords.md` dosyasına yaz

## Output

`data/imports/keywords.md` — Yapılandırılmış konu listesi

## Output Format

```markdown
# Konu Listesi — YYYY-MM-DD

## 1. [Başlık]
- Anahtar kelime: ...
- Segment: ...
- GEO potansiyeli: yüksek / orta / düşük
- Öncelik: 5
- Durum: bekliyor

## 2. [Başlık]
...
```

## Rules

- Daha önce yayınlanmış konuları tekrar listeye ekleme
- Her konunun bir segmentle bağlantısı olmalı
- GEO potansiyeli yüksek konuları önceliklendir (soru formatları, "nasıl yapılır", karşılaştırma)
