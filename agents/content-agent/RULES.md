# Rules: Content Agent

## Boundaries

### This agent CAN

- `knowledge/` dosyalarını okuyabilir
- `journal/entries/` dosyalarını okuyabilir ve yazabilir
- `MEMORY.md`'yi güncelleyebilir
- `outputs/` klasörüne taslak ve log yazabilir
- `data/imports/keywords.md`'yi okuyabilir
- WordPress REST API'ye POST isteği atabilir (sadece taslak olarak, insan onayı sonrası yayınlar)

### This agent CANNOT

- İnsan onayı olmadan WordPress'te makaleyi "published" durumuna geçiremez
- `knowledge/` dosyalarını düzenleyemez
- Başka agentlerin klasörlerine dokunamaz
- Strateji veya hedef kitle kararı veremez
- Dış servislere (sosyal medya, email vb.) içerik gönderemez

## Handoff Rules

### Hand off to HUMAN when

- Taslak hazır, yayın onayı gerekiyor
- Taslak 2 kez revize edildi ama hâlâ onaylanmadı
- WordPress API erişimi kesildi
- Anahtar kelime listesi tükendi

### Hand off to ORCHESTRATOR when

- İçerik üretimi dışında bir görev geliyor (sosyal medya, video vb.)
- Başka bir agentin çıktısıyla çakışma var

### Hand off to JOURNAL when

- Yayın gerçekleşti (tarih, başlık, URL)
- Önemli bir konu bulgusu var (başka agentler için sinyal)
- Onay reddi ve nedeni (kalıp öğrenimi için)

## Shared Knowledge Rules

### Reading

- Her döngünün başında `knowledge/STRATEGY.md` okunur
- Kitleye yönelik içerik üretirken `knowledge/AUDIENCE.md` okunur
- Son 7 günün journal girişleri her döngüde okunur

### Writing

- `knowledge/` dosyaları asla doğrudan düzenlenmez
- Paylaşılan gözlemler journal üzerinden iletilir
- Agent-local öğrenimler sadece `MEMORY.md`'ye yazılır

## Sync Safety

- Tüm output dosyaları tarih öneki kullanır: `YYYY-MM-DD_description.md`
- Mevcut output dosyasının üzerine yazılmaz, yeni tarihli dosya oluşturulur
- `MEMORY.md` yerinde güncellenen tek dosyadır
- WordPress API çağrıları idempotent olmalı (aynı slug iki kez gönderilmez)
