# Firebase kurulumu (ortak tahmin listesi)

Site Firebase olmadan da çalışır (tahmin sadece kendi tarayıcıda görünür). Ortak liste için:

1. https://console.firebase.google.com adresinde yeni bir proje oluştur (Analytics gerekmez).
2. **Build → Authentication → Sign-in method → Anonymous** seçeneğini etkinleştir.
3. **Build → Firestore Database → Create database** (production mode, bölge: `eur3` ya da yakın biri).
4. Firestore **Rules** sekmesine `firestore.rules` dosyasının içeriğini yapıştırıp **Publish** et.
5. **Project settings → General → Your apps → Web (`</>`)** ile bir web uygulaması ekle,
   çıkan `firebaseConfig` değerlerini `index.html` içindeki `FIREBASE_CONFIG` sabitine yapıştır:

   ```js
   const FIREBASE_CONFIG = { apiKey: "...", authDomain: "...", projectId: "...", appId: "..." };
   ```
6. **Authentication → Settings → Authorized domains** listesine siteyi yayınladığın alan adını ekle
   (örn. `suleyman-kara.github.io`).

Notlar
- `apiKey` gizli bir anahtar değildir, istemci kodunda durması normaldir. Güvenliği Firestore kuralları sağlar.
- "Tarayıcı başına 1 tahmin" anonim kullanıcı kimliğiyle sağlanır. Site verisini silen ya da gizli sekme
  kullanan biri yeni bir tahmin hakkı kazanır; bu bir şaka sitesi için kabul edilebilir bir sınırdır.
- Kötü niyetli kullanımı sınırlamak için Firebase konsolunda App Check ya da bütçe uyarısı eklenebilir.
