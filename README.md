# SEOUL SNAP — Browser Photobooth Demo

Photobooth operasional berbasis browser: countdown, 10 foto digital per sesi, pilihan frame, pemilihan 2–4 foto untuk dicetak, unduhan tiap foto, unduhan batch 10 foto, QR code sesi, dan dialog cetak.

## Jalankan di Windows

**Cara paling mudah (VS Code):**
1. Ekstrak folder `seoul-photobooth`.
2. Buka folder ini di VS Code.
3. Install ekstensi **Live Server** (Ritwick Dey) bila belum ada.
4. Klik kanan `index.html` → **Open with Live Server**.
5. Browser akan membuka alamat localhost. Tekan **MULAI PHOTOBOOTH** untuk demo.

Bisa juga menggunakan Python jika sudah terpasang:
```bash
python -m http.server 8000
```
Lalu buka `http://localhost:8000` di browser.

## Kamera
Klik ikon ⚙ → pilih **Kamera perangkat**, simpan, lalu izinkan akses webcam. Akses kamera memerlukan `localhost` atau HTTPS. Jika kamera belum ada, pilih Demo.

## Cetak
Ambil 10 foto digital, lalu pilih 2, 3, atau 4 foto di panel pilihan untuk layout cetak. Setiap foto dapat diunduh sendiri-sendiri; tombol unduh 10 foto akan meminta izin browser untuk beberapa unduhan. Klik **Cetak photo strip** atau **Cetak sekarang**. Browser membuka dialog cetak dan pengguna perlu memilih printer serta mengonfirmasi. Browser web biasa tidak mengizinkan cetak diam-diam tanpa konfirmasi.

## QR code dan batasan demo
QR saat ini berisi alamat halaman aplikasi (bukan file foto). Untuk pelanggan memindai QR lalu mengambil foto dari ponsel lain, aplikasi perlu di-host melalui HTTPS dan perlu backend/storage untuk mengunggah hasil foto serta membuat tautan sesi unik. QR memakai pustaka CDN, sehingga QR memerlukan koneksi internet.

## Catatan penting
- Mode demo menggambar visual simulasi; foto bukan foto orang sungguhan.
- File unduhan dibuat di browser dan tidak diunggah ke server.
- Cetak di browser adalah alur cetak manual melalui dialog sistem. Silent/automatic printing biasanya memerlukan konfigurasi kiosk/desktop khusus dan printer yang sudah disiapkan.
- Ini starter yang dapat dijalankan, belum sistem produksi untuk operasional komersial.

## Live preview dari kamera HP ke PC tanpa memasang aplikasi
Folder ini juga memiliki dua halaman eksperimental:
- `pc-camera.html` dibuka di PC untuk mendapatkan ID koneksi.
- `phone-camera.html` dibuka di browser HP, lalu masukkan ID PC dan aktifkan kamera.

**Batasan penting:** kedua halaman harus diakses lewat hosting **HTTPS** (misalnya deploy folder ini ke layanan hosting statis yang memberi HTTPS). Membuka halaman dari alamat LAN `http://192.168.x.x` biasanya tidak diizinkan memakai kamera HP karena `getUserMedia` memerlukan secure context. Koneksi PeerJS memakai layanan signaling internet; kedua perangkat perlu internet. Tidak perlu memasang aplikasi di HP atau PC, tetapi ini bukan koneksi offline sepenuhnya. Ini live preview terpisah; belum otomatis mengalirkan frame ke sesi foto utama `index.html`.


## Kamera HP ke halaman utama
1. Deploy repository ke Vercel agar memakai HTTPS.
2. Di PC, buka halaman utama `index.html` melalui alamat Vercel.
3. Tekan **AKTIFKAN KONEKSI HP** dan tunggu ID muncul.
4. Di HP, buka `/phone-camera.html`, tekan **Aktifkan kamera HP**, masukkan ID dari PC, lalu tekan **Hubungkan**.
5. Kembali ke halaman utama di PC. Live preview harus muncul di area kamera.

Koneksi video memakai PeerJS dan membutuhkan internet untuk signaling; izin kamera di HP harus diizinkan. Ini masih prototipe browser, bukan sistem kamera lokal/offline.
