 İsim - Soy isim Necmihan AKSU
Öğrenci No:250541086
// Başlangıç Verileri
DEĞİŞKEN Bakiye = 2000
DEĞİŞKEN Gunluk_Limit = 1000
DEĞİŞKEN Cekilen_Miktar_Bugun = 0

BAŞLA
    EKRANA_YAZ "ATM Para Çekme İşlemi"
    EKRANA_YAZ "Hesap Bakiyesi: " + Bakiye + " TL"
    EKRANA_YAZ "Güncel Günlük Çekme Limiti: " + (Gunluk_Limit - Cekilen_Miktar_Bugun) + " TL"

    DÖNGÜ:
        EKRANA_YAZ "Çekmek istediğiniz miktarı girin (TL):"
        OKU Cekilecek_Miktar

        // 1. Geçerli Para Birimi Kontrolü (Opsiyonel: 10, 20 gibi banknot katları)
        EĞER Cekilecek_Miktar <= 0 O ZAMAN
            EKRANA_YAZ "Hata: Geçerli bir miktar girin."
            ATLA DÖNGÜ BAŞLANGICINA

        // 2. Günlük Limit Kontrolü
        EĞER Cekilecek_Miktar > (Gunluk_Limit - Cekilen_Miktar_Bugun) O ZAMAN
            EKRANA_YAZ "Hata: Günlük çekme limitinizi aşıyorsunuz."
            EKRANA_YAZ "Kalan Günlük Limit: " + (Gunluk_Limit - Cekilen_Miktar_Bugun) + " TL"
            ATLA DÖNGÜ BAŞLANGICINA

        // 3. Bakiye Kontrolü
        EĞER Cekilecek_Miktar > Bakiye O ZAMAN
            EKRANA_YAZ "Hata: Hesap bakiyeniz yetersiz."
            EKRANA_YAZ "Hesap Bakiyesi: " + Bakiye + " TL"
            ATLA DÖNGÜ BAŞLANGICINA

        // 4. İşlem Başarılı
        Bakiye = Bakiye - Cekilecek_Miktar
        Cekilen_Miktar_Bugun = Cekilen_Miktar_Bugun + Cekilecek_Miktar

        EKRANA_YAZ Cekilecek_Miktar + " TL çekildi."
        EKRANA_YAZ "Yeni Hesap Bakiyesi: " + Bakiye + " TL"
        EKRANA_YAZ "Kalan Günlük Limit: " + (Gunluk_Limit - Cekilen_Miktar_Bugun) + " TL"

        EKRANA_YAZ "Başka işlem yapmak istiyor musunuz? (Evet/Hayır)"
        OKU Cevap

        EĞER Cevap = "Hayır" VEYA Cevap = "HAYIR" O ZAMAN
            DÖNGÜDEN_ÇIK
        
    DÖNGÜ BİTİŞİ

    EKRANA_YAZ "İyi günler dileriz."
SON
sistemin kısa açıklaması (maks. 5-6 satır) Bu sistem, 2000 TL bakiyesi ve 1000 TL günlük çekme limiti olan bir ATM işlemini simüle eder. Kullanıcıdan çekim miktarı istenir ve bu miktar 20 TL'nin katı olmalıdır. Ardından, günlük limit ve bakiye kontrol edilir. Tüm şartlar sağlanırsa para verilir ve bakiye güncellenir; aksi takdirde kullanıcıya ilgili hata mesajı gösterilerek tekrar denemesi istenir.
