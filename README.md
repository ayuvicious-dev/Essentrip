# Essentrip

Aplikasi PWA untuk merencanakan perjalanan: daftar trip, itinerary, catatan biaya vs budget, dan packing list.
Dibangun dengan HTML/CSS/JS murni + Firebase (Authentication & Cloud Firestore). Di-host di GitHub Pages.

## Struktur
- `index.html` – seluruh aplikasi
- `manifest.json`, `service-worker.js` – PWA (bisa di-install, tampil offline)
- `icons/` – ikon & logo
- `.nojekyll` – agar GitHub Pages menyajikan file apa adanya

## Setup Firebase
1. Console → Authentication → Sign-in method → aktifkan **Email/Password**.
2. Authentication → Settings → Authorized domains → tambahkan `USERNAME.github.io`.
3. Firestore Database → Rules → tempel lalu **Publish**:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

## Deploy
Upload semua file ke repo GitHub → Settings → Pages → Deploy from branch (`main`, folder `/root`).
Setelah revisi, naikkan versi `CACHE` di `service-worker.js` agar pengguna mendapat update.
