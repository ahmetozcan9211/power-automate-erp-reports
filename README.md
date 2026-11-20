# Power Automate ERP Raporlama ve Uyarıları

Power Automate Desktop (PAD), Power Automate bulut akışları ve Excel Office Scripts kullanılarak kurulmuş raporlama ve kontrol otomasyonları.

> Bu depo bir proje vitrinidir. Kaynak kod ve akışlar paylaşılmamaktadır.

## Mimari

PAD bir makinede aynı anda tek akış çalıştırabildiği için tüm otomasyonlar tek bir **orkestratör akışta** alt akışlar olarak durur:

```
organizer
 ├─ Main            5 dk'lık döngü, alt akışları sırayla çağırır
 ├─ SqlHazirla      SQL şablonlarındaki yer tutucuları doldurur
 ├─ IzinliVaryant   izin listesi dışı varyant seçimi → Telegram uyarısı
 └─ SatisRaporu     her gün 18:00 günlük satış raporu → Telegram
```

Her alt akış kendi hata bloğu içinde çalışır. Biri hata verse de diğerleri çalışmaya devam eder ve bir sonraki turda yeniden denenir. Hiçbir akış veritabanına yazmaz.

## Bulut bileşenleri

- **Office Scripts (TypeScript):** SharePoint'teki Excel dosyalarında varyant kontrolü, iş emri giriş kontrolü, işçilik güncelleme, satış raporu
- **SharePoint listeleri ve Excel** kullanıcı arayüzü olarak kullanılır
- **Python yardımcıları:** SQL üretimi, ilk veri yüklemesi, dosya birleştirme
- Ayarlar (bot token, sohbet ID, bağlantı) koddan ayrı, Excel ayar sayfasında tutulur

## Teknolojiler

`Power Automate Desktop` · `Power Automate Cloud` · `Office Scripts (TypeScript)` · `SharePoint` · `ODBC / PostgreSQL` · `Telegram Bot API` · `Python`
