# Sınıf Kütüphanesi — Android APK

Bu klasör, telefonda gerçek bir uygulama (APK) olarak çalışacak sınıf
kütüphane takip programının kaynak kodudur. Veriler tamamen **telefonun
kendi hafızasında** (localStorage) tutulur, internet gerekmez.

## En kolay yol: GitHub Actions ile otomatik derleme (Android Studio kurmadan)

1. [github.com](https://github.com) üzerinde ücretsiz bir hesap açın (yoksa).
2. Yeni bir **repository (depo)** oluşturun, örneğin `sinif-kutuphanesi`.
3. Bu klasördeki **tüm dosyaları** o depoya yükleyin (GitHub'ın web
   arayüzünden "Add file → Upload files" ile sürükle-bırak yapabilirsiniz,
   veya `git` biliyorsanız `git push` ile).
4. Depoda üstteki **Actions** sekmesine girin. "APK Derle" iş akışını
   göreceksiniz. Otomatik başlamazsa **Run workflow** butonuna basın.
5. Derleme ~3-5 dakika sürer. Bittiğinde sayfanın altında
   **Artifacts → sinif-kutuphanesi-apk** dosyasını indirin. İçinden çıkan
   `app-debug.apk` dosyasını telefonunuza aktarıp kurabilirsiniz
   (Android'de "bilinmeyen kaynaklardan yükleme" iznini açmanız gerekebilir).

Bu yöntemde bilgisayarınıza hiçbir şey kurmanız gerekmez — derleme işini
GitHub'ın sunucuları yapar.

## Alternatif: Kendi bilgisayarınızda derlemek isterseniz

Gereksinimler: Node.js, Android Studio (Android SDK için), Java 17.

```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

APK şurada oluşur: `android/app/build/outputs/apk/debug/app-debug.apk`

## Uygulama nasıl kullanılır?

- **Kitaplar** sekmesi: Excel dosyasından toplu kitap ekleyin (sütun:
  "Kitap Adı", isteğe bağlı "Yazar") veya tek tek elle ekleyin. Her kitap
  için otomatik bir QR kod üretilir — bunları yazdırıp kitapların içine
  yapıştırın.
- **Öğrenciler** sekmesi: Excel'den toplu öğrenci ekleyin (sütun:
  "Ad Soyad") veya tek tek elle ekleyin.
- **Ödünç/İade**: Öğrenciyi listeden seçin, kitabın QR kodunu kameraya
  gösterin. Aynı kitap tekrar okutulunca otomatik iade olarak işlenir.
- **Durum**: Kimde hangi kitap var ve tüm işlem geçmişi.

## Not

Play Store'a yayınlamak isterseniz uygulamayı imzalamanız (signed release
build) ve bir Google Play Console hesabı açmanız gerekir — bu adım farklı
bir süreçtir, isterseniz onu da ayrıca anlatabilirim.
