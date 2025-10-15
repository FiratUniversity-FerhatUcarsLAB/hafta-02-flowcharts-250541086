Necmihan AKSU
250541086





// Başlangıç Verileri ve Kurallar
DEĞİŞKEN Musteri_Kredisi = 30 // Bir dönemde alınabilecek maksimum kredi
DEĞİŞKEN Alinan_Kredi = 0
DEĞİŞKEN Secilen_Dersler: Liste
DEĞİŞKEN Mevcut_Dersler: Veritabanı // Ders Kodu, Kredi, Kontenjan, Önkoşul Bilgisi içerir

PROSEDÜR Ders_Kayit_Sistemi
BAŞLA
    EKRANA_YAZ "Üniversite Ders Kayıt Sistemine Hoş Geldiniz."

    DÖNGÜ:
        EKRANA_YAZ "1. Ders Ekle, 2. Ders Sil, 3. Kaydı Tamamla, 4. Çıkış"
        OKU Secim

        EĞER Secim = 1 O ZAMAN
            ÇAĞIR PROSEDÜR Ders_Ekle()
        YOKSA EĞER Secim = 2 O ZAMAN
            ÇAĞIR PROSEDÜR Ders_Sil()
        YOKSA EĞER Secim = 3 O ZAMAN
            ÇAĞIR PROSEDÜR Kaydi_Tamamla()
            DÖNGÜDEN_ÇIK
        YOKSA EĞER Secim = 4 O ZAMAN
            EKRANA_YAZ "Kayıt Yapılmadan Çıkılıyor."
            DÖNGÜDEN_ÇIK
        YOKSA
            EKRANA_YAZ "Geçersiz seçim. Tekrar deneyin."
        BİTİR EĞER
    DÖNGÜ BİTİŞİ
SON

PROSEDÜR Ders_Ekle()
    EKRANA_YAZ "Eklemek istediğiniz dersin kodunu girin:"
    OKU DersKodu

    DersBilgisi = DersKodu'na göre Mevcut_Dersler'i Sorgula
    
    EĞER DersBilgisi BOŞ O ZAMAN
        EKRANA_YAZ "Hata: Ders kodu bulunamadı."
        GERİ_DÖN
    BİTİR EĞER

    // Kontrol 1: Önkoşul Kontrolü
    EĞER DersBilgisi.Onkosul GECILMEDI O ZAMAN
        EKRANA_YAZ "Hata: Bu dersi almak için önkoşul dersi (" + DersBilgisi.Onkosul + ") geçilmelidir."
        GERİ_DÖN
    BİTİR EĞER

    // Kontrol 2: Kredi Kontrolü
    EĞER (Alinan_Kredi + DersBilgisi.Kredi) > Musteri_Kredisi O ZAMAN
        EKRANA_YAZ "Hata: Kredi limitinizi (" + Musteri_Kredisi + ") aşıyorsunuz."
        GERİ_DÖN
    BİTİR EĞER

    // Kontrol 3: Kontenjan Kontrolü
    EĞER DersBilgisi.Kontenjan <= 0 O ZAMAN
        EKRANA_YAZ "Hata: Dersin kontenjanı dolmuştur."
        GERİ_DÖN
    BİTİR EĞER

    // Ekleme İşlemi Başarılı
    Secilen_Dersler'e DersKodu'nu Ekle
    Alinan_Kredi = Alinan_Kredi + DersBilgisi.Kredi
    DersBilgisi.Kontenjan = DersBilgisi.Kontenjan - 1
    EKRANA_YAZ DersKodu + " başarıyla eklendi. Toplam Kredi: " + Alinan_Kredi
BİTİR PROSEDÜR

PROSEDÜR Kaydi_Tamamla()
    EĞER Secilen_Dersler BOŞ DEĞİL O ZAMAN
        EKRANA_YAZ "Ders kaydınız başarıyla onaylanmıştır. Seçilen Dersler: " + Secilen_Dersler
    YOKSA
        EKRANA_YAZ "Hata: Sepetinizde ders bulunmamaktadır."
    BİTİR EĞER
BİTİR PROSEDÜR

sistemin kısa açıklaması (maks. 5-6 satır)
Bu sistem, öğrencilerin üniversite derslerini seçmesine olanak tanır. Her ders ekleme işleminde sırasıyla önkoşul, toplam kredi limiti (30 kredi) ve dersin kontenjanı kontrol edilir. Tüm kurallar sağlanırsa ders sepete eklenir ve öğrenci kaydını onaylayabilir. Başarısız her kontrol, kullanıcıya ilgili hatayı bildirir ve işlemi sonlandırır.


