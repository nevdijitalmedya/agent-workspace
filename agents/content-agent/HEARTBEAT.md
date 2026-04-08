# Content Agent Heartbeat

## Schedule

Günlük (sabah çalışır). Haftalık review her Pazartesi.

## Each Cycle

### 1. Read Context

- `journal/entries/` — Son 7 günün girişlerini kontrol et
- `knowledge/STRATEGY.md` — Öncelik değişikliği var mı?
- `MEMORY.md` — Geçmiş döngülerden öğrenimler
- `data/imports/keywords.md` — İnsan tarafından eklenmiş yeni konu var mı?

### 2. Assess State

- Yayınlanmayı bekleyen onaylı taslak var mı? → WP_PUBLISH çalıştır
- Onay bekleyen taslak var mı? → İnsana bildir, bekle
- Taslak pipeline'ı boş mu? → TOPIC_RESEARCH → CONTENT_GENERATE çalıştır
- Yayınlanan içerik 7 günü geçti mi? → SEO_AUDIT çalıştır

### 3. Execute Skill

```text
keywords.md'de konu var
  └─ CONTENT_GENERATE → taslak kaydet
       └─ IMAGE_GENERATE → görsel üret → WP media'ya yükle → taslağa featured_image_id ekle
            └─ insan onayı iste

Onaylı taslak var (featured_image_id dahil)
  └─ WP_PUBLISH → yayın logu kaydet → journal'a yaz

Pipeline boş
  └─ TOPIC_RESEARCH → MEMORY.md ve data/imports/ güncelle

Yayınlanan içerik 7 gün geçti
  └─ SEO_AUDIT → journal'a yaz
```

### 4. Log to Journal

- Bu döngüde ne yapıldı
- Onay bekleyen taslak sayısı
- Bir sonraki döngüde ne yapılmalı

## Weekly Review (Her Pazartesi)

### 1. Gather Data

- `outputs/` klasöründeki son 7 günün yayın loglarını oku
- `journal/entries/` son 7 günü oku

### 2. Score Against Targets

| Metric | Target | This Week | Status |
| --- | --- | --- | --- |
| Üretilen taslak | 2/hafta | | |
| Onaylanan taslak | >%80 | | |
| Yayınlanan makale | 2/hafta | | |

### 3. Analyze Wins and Misses

- **Wins:** Hangi konu formatları hızlı onaylandı? MEMORY.md'ye yaz.
- **Misses:** Hangi taslaklar reddedildi veya revize edildi? Nedenini MEMORY.md'ye yaz.

### 4. Update Memory

Doğrulanan formatları, çalışan konu kalıplarını MEMORY.md'ye ekle.

### 5. Log Weekly Summary to Journal

- Üretilen / onaylanan / yayınlanan makale sayısı
- En iyi performans gösteren konu
- Gelecek hafta için öneri

## Escalation Rules

- 2 ardışık hafta taslak onay oranı <%50 → İnsana eskal et
- WordPress API bağlantısı başarısız → İnsana bildir
- Anahtar kelime listesi 2 haftadır güncellenmedi → İnsana hatırlat
- Bir konu hiçbir skill'e uymuyorsa → Orchestrator'a ilet

## Rules

- Her döngüde önce journal'ı oku
- Onay almadan WordPress'e yayın yapma
- Bir döngüde tek skill çalıştır (yayın + audit istisnası)
- Hedeflere hizmet etmeyen taslak üretme
