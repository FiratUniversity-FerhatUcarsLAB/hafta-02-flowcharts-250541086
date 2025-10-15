Necmihan AKSU
250541086
// Veri Yapısı Tanımlamaları
YAPI Urun:
    DEĞİŞKEN UrunID: TamSayı
    DEĞİŞKEN Ad: Metin
    DEĞİŞKEN Fiyat: OndalıkSayı
    DEĞİŞKEN Stok: TamSayı

DEĞİŞKEN Sepet: Liste (Urun nesneleri tutar)

// Ana Prosedür
PROSEDÜR Alisveris_Sepeti_Sistemi
BAŞLA
    Sepet = Yeni Liste()
    
    DÖNGÜ:
        EKRANA_YAZ "1. Ürün Ekle, 2. Ürün Sil, 3. Sepeti Görüntüle, 4. Toplamı Hesapla, 5. Çıkış"
        OKU Secim

        EĞER Secim = 1 O ZAMAN
            ÇAĞIR PROSEDÜR Urun_Ekle(Sepet)
        YOKSA EĞER Secim = 2 O ZAMAN
            ÇAĞIR PROSEDÜR Urun_Sil(Sepet)
        YOKSA EĞER Secim = 3 O ZAMAN
            ÇAĞIR PROSEDÜR Sepeti_Goruntule(Sepet)
        YOKSA EĞER Secim = 4 O ZAMAN
            ÇAĞIR PROSEDÜR Toplami_Hesapla(Sepet)
        YOKSA EĞER Secim = 5 O ZAMAN
            DÖNGÜDEN_ÇIK
        YOKSA
            EKRANA_YAZ "Geçersiz seçim. Lütfen tekrar deneyin."
        BİTİR EĞER
    DÖNGÜ BİTİŞİ
    
    EKRANA_YAZ "Sepet İşlemleri Sonlandı."
SON

// Yardımcı Prosedürler
PROSEDÜR Urun_Ekle(Sepet)
    // Basitlik için ürün detaylarının dışarıdan geldiği varsayılır.
    EKRANA_YAZ "Eklemek istediğiniz Ürün ID ve Adedini girin:"
    OKU YeniUrunID, YeniUrunAdedi

    // Gerçek bir sistemde stok kontrolü yapılır.
    
    YENİ_URUN = Urun nesnesi oluştur (ID, Adet, Fiyat bilgileriyle)
    Sepet'e YENİ_URUN'u ekle
    EKRANA_YAZ "Ürün sepete eklendi."
BİTİR PROSEDÜR

PROSEDÜR Toplami_Hesapla(Sepet)
    DEĞİŞKEN ToplamTutar = 0
    HER_URUN İÇİN Sepet'te
        ToplamTutar = ToplamTutar + (HER_URUN.Fiyat * HER_URUN.Adet)
    BİTİR HER_URUN
    
    EKRANA_YAZ "Sepet Toplamı: " + ToplamTutar + " TL"
    DÖN ToplamTutar // Toplam tutarı döndür
BİTİR PROSEDÜR
sistemin kısa açıklaması (maks. 5-6 satır)
Bu sistem, bir online alışveriş sepetinin temel işlevlerini yönetir. Kullanıcıya ürün ekleme, sepetten ürün silme, sepet içeriğini ve toplam tutarı görüntüleme seçeneklerini sunan döngüsel bir menü bulunur. Sepete eklenen her ürünün adedi ve fiyatı üzerinden sepetin toplam maliyeti hesaplanır. Sistem, kullanıcı "Çıkış" seçeneğini seçene kadar çalışmaya devam 
