# FULK — Spesifikasi Induk Produk dan Implementasi
Versi dokumen: 1.0 | Application ID: `id.fulk.app` | Target: Android native

## 0. Aturan utama proyek
1. Bangun aplikasi Android native dengan Kotlin + Jetpack Compose, kecuali ada alasan teknis kuat yang dijelaskan sebelum mengubah stack.
2. Jangan mengubah konsep, alur, bobot, landasan Qur’ani, nama fitur, logo, atau keputusan pengguna yang tercantum di dokumen ini tanpa persetujuan eksplisit.
3. Jangan membuat tombol palsu, data statistik rekaan, status verifikasi palsu, atau mengklaim integrasi berfungsi jika belum diimplementasikan dan diuji.
4. Jika fungsi memerlukan API eksternal, kredensial, izin Android, layanan backend, atau kebijakan khusus OS, implementasikan integrasi yang nyata jika mungkin; jika belum dapat dijalankan, sediakan adapter yang jelas, jelaskan prasyaratnya, dan jangan menyamarkannya sebagai fungsi aktif.
5. Prioritaskan keselamatan data, privasi, aksesibilitas, pengujian, dan dokumentasi. Jangan pernah menaruh API key di source code atau repositori.
6. Deliverable bukan hanya mockup. Berikan source code lengkap, build instructions, pengujian, serta APK hanya bila build benar-benar berhasil.

## 1. Identitas, platform, dan desain
- Nama produk: FULK.
- Application ID: `id.fulk.app`.
- Target awal: Android; pengembangan melalui Claude AI dan GitHub Codespaces/browser.
- Stack yang diinginkan: Kotlin, Jetpack Compose, Gradle Kotlin DSL.
- Logo resmi: gambar perisai biru-putih yang diberikan pengguna, berisi simbol gelombang/bahtera putih. Gunakan file logo asli apa adanya: jangan menggambar ulang, mengubah warna/bentuk/proporsi, memotong, atau meregangkan. Buat ukuran aset berbeda hanya dengan scaling proporsional dan padding yang sesuai. Jika file logo belum tersedia pada proyek, minta pengguna mengunggahnya; jangan mengganti dengan logo rekaan.
- Beranda: modern, minimalis, hangat; header gradasi biru dengan gelombang abstrak; dua kartu ringkasan berdampingan; enam kartu fitur dalam grid 3 kolom × 2 baris; tanpa bagian aktivitas tambahan di bawah grid; navigasi bawah perlu sederhana dan konsisten. Pastikan grid tetap terbaca di layar sempit—boleh gunakan layout adaptif yang menjaga maksud desain.
- Jangan tampilkan kapal/ornamen Qur’ani besar di beranda. FULK Reflect secara khusus menggunakan visual bahtera dan level air.
- Tema: `System default`, `Light`, `Dark`. Simpan pilihan pengguna; perubahan tema harus memengaruhi seluruh layar dan dialog. Logo asli tetap biru-putih dan ditempatkan pada latar yang menjaga kontras.
- Palet visual mengikuti logo biru-putih dengan navy dan latar terang lembut. Hindari tampilan ramai.
- Layar pembuka Qur’ani tampil setiap kali pengguna membuka salah satu dari enam fitur: nama fitur, teks Arab yang diverifikasi, terjemahan Indonesia yang diverifikasi, referensi surah/ayat, penjelasan relevansi ringkas, lalu tombol `Lanjutkan` menuju fitur. Jangan memaksakan makna ayat. Sediakan aksesibilitas teks dan ukuran huruf.
- Sumber teks Arab dan terjemahan harus diverifikasi dari sumber tepercaya sebelum shipping; jangan mengandalkan teks yang dibuat model tanpa pemeriksaan.

## 2. Enam fitur dan landasan Qur’ani

### 2.1 FULK Time
**Landasan:** QS al-‘Aṣr [103]: 1–3 — kesadaran dan pemanfaatan waktu.
Fungsi:
- Pengguna mengatur batas pemakaian aplikasi digital/media sosial.
- Menampilkan riwayat penggunaan yang benar-benar dapat diperoleh.
- Mengirim pengingat sebelum batas terlampaui. Contoh yang disepakati: bila batas 2 jam, pengingat pada menit ke-110.
- Smart Pause tampil sebagai overlay/pop-up di atas aplikasi media sosial yang sedang digunakan jika izin dan mekanisme Android memungkinkan.
- Pilihan `Ambil jeda 1 menit` menjalankan jeda terukur, lalu menyediakan alur setelah jeda.
- Pilihan `Saya ingin melanjutkan penggunaan` tidak boleh mengembalikan pengguna langsung ke media sosial. Arahkan ke FULK Learn → modul `Mengenali Ancaman dan Manipulasi`. Tidak ada tombol untuk melewati pembelajaran. Setelah pelajaran dan evaluasi selesai, lanjutkan alur sesuai desain yang telah disepakati.
- Jangan mengklaim mendeteksi pola scrolling tanpa tujuan kecuali mekanisme pendeteksian tersebut sungguh dibuat dan diuji. Implementasi awal yang realistis adalah pemicu berdasarkan durasi.
Implementasi:
- Jelaskan izin Usage Access/overlay dan langkah mengaktifkannya; jangan mencoba melewati proteksi Android.
- Jika overlay di atas aplikasi lain tidak dapat aktif sebelum izin diberikan, tampilkan onboarding dan status izin yang nyata.
- Sediakan penanganan izin dicabut, restart perangkat, dan aplikasi target tidak terdeteksi.
- Jangan membuat kontrol tersembunyi yang mengganggu atau memaksa di luar alur yang disepakati.

### 2.2 FULK Shield
**Landasan:** QS al-Baqarah [2]:188 — larangan memperoleh harta secara batil; dikontekstualisasikan untuk penipuan/phishing digital, bukan diklaim membahas teknologi secara literal.
Fungsi:
- Membantu pengguna menghadapi phishing, penipuan daring, promosi judi daring, dan konten digital berbahaya.
- Saat tautan atau tindakan berisiko dikenali oleh mekanisme nyata, tampilkan peringatan yang menjelaskan indikator risiko dan opsi aman.
- Jangan mengklaim setiap tautan dapat dideteksi. Nyatakan keterbatasan cakupan sumber dan pemindaian.
- Tutorial pemblokiran satu situs pada perangkat Redmi/HyperOS telah dibahas. Panduan harus dapat disesuaikan dengan versi OS dan menjelaskan keterbatasan DNS, browser, serta pemblokiran tingkat perangkat. Jangan menyatakan situs terblokir sebelum pengguna memverifikasi.
- Pisahkan Shield (perlindungan/peringatan keamanan) dari Check (pemeriksaan klaim/kebenaran informasi).

### 2.3 FULK Check
**Landasan:** QS al-Ḥujurāt [49]:6 — tabayyun/verifikasi informasi.
Fungsi:
- Mengutamakan pemeriksaan otomatis melalui sumber atau layanan verifikasi yang benar-benar tersedia; bukan chatbot AI yang berpura-pura memiliki akses atau kepastian.
- Pengguna memasukkan teks klaim atau URL; validasi input, tampilkan status proses, sumber yang diperiksa, waktu pemeriksaan, ringkasan hasil, dan keterbatasan.
- Bedakan status seperti `didukung sumber`, `dibantah sumber`, `belum cukup bukti`, dan `gagal memeriksa`; jangan memaksa hasil biner benar/salah jika bukti tidak memadai.
- Tautkan sumber rujukan bila tersedia. Jangan membuat sumber, kutipan, atau hasil verifikasi palsu.
- Implementasi memerlukan penyedia/API/backend atau metode pencarian yang sah. Gunakan interface provider dan konfigurasi aman. Jika API key belum tersedia, UI harus menyebut bahwa pemeriksaan online belum dikonfigurasi, bukan menghasilkan hasil rekaan.
- Simpan riwayat pemeriksaan sesuai pengaturan privasi pengguna.

### 2.4 Suara FULK
**Landasan:** QS al-Mā’idah [5]:2 — ta‘āwun/saling membantu dalam kebaikan.
Fungsi:
- Pengguna dapat melaporkan informasi atau aktivitas bermasalah.
- Form laporan memuat objek/link, kategori, alasan, bukti/sumber opsional, dan konfirmasi.
- Pengguna dapat melihat status laporan, waktu pembaruan, dan sumber verifikasi yang tersedia.
- Laporan yang sudah diperiksa dapat membantu pengguna lain melalui daftar publik/berbagi ancaman, tetapi jangan tampilkan laporan mentah seolah sudah terbukti.
- Status harus jelas, misalnya `Diterima`, `Dalam pemeriksaan`, `Terverifikasi`, `Tidak cukup bukti`, `Ditolak`, `Gagal diproses`.
- Implementasi multi-pengguna membutuhkan backend/database dan moderasi. Jangan menyimulasikan laporan publik lintas pengguna dengan data lokal seolah merupakan sistem komunitas nyata.
- Jangan mengirim laporan ke pihak eksternal tanpa persetujuan pengguna dan penjelasan tujuan.

### 2.5 FULK Reflect — spesifikasi terkunci v1.0
**Landasan:** QS al-Ḥasyr [59]:18 — muhasabah dan mempersiapkan hari esok.
Tujuan: refleksi kebiasaan digital, ringkasan aktivitas, dan progres visual menggunakan bahtera serta level air. Air adalah metafora desain, bukan ukuran klinis atau ukuran langsung epistemic flooding.

Aturan final:
- Masa tenggang: 2 hari berturut-turut tanpa aktivitas bermakna.
- Setelah masa tenggang, air naik 10 poin persentase per hari tidak aktif.
- Batas level air: 100%.
- Setiap 1 poin aktivitas mengurangi air 5 poin persentase.
- Bobot aktivitas:
  - menyelesaikan satu modul FULK Learn: 3 poin;
  - menyelesaikan pemeriksaan klaim FULK Check: 3 poin;
  - melakukan Smart Pause/pengelolaan paparan: 2 poin;
  - menyelesaikan refleksi FULK Reflect: 2 poin;
  - laporan mandiri pengurangan penggunaan media sosial: 1 poin.
- Karena pengurangan air 5% per poin, nilai aktivitas di atas mengurangi air 15%, 15%, 10%, 10%, dan 5% secara berurutan.
- Membuka aplikasi saja tidak menambah poin dan tidak membuat air surut.
- Aktivitas harus benar-benar selesai dan deduplikasi harus mencegah penghitungan ulang tidak sah.
- Misi harian direset saat hari baru; progres dan riwayat jangka panjang tidak dihapus karena absen.
- Ketidakaktifan tidak boleh menghapus pencapaian atau mempermalukan pengguna.
- Data penggunaan nyata, laporan mandiri, dan aktivitas yang diselesaikan harus dibedakan. Jangan mengarang durasi, jumlah ancaman, atau pengurangan paparan.
- Notifikasi: satu pengingat utama pada waktu yang dipilih pengguna jika belum ada aktivitas bermakna; maksimal satu pengingat lanjutan opsional; total maksimum dua notifikasi Reflect per hari. Pengguna bisa mengatur waktu, jam tenang, menunda, atau mematikan notifikasi.
- Notifikasi tidak dihitung sebagai aktivitas.
- Ringkasan mingguan hanya berisi data yang sungguh tercatat, dengan label jelas untuk laporan mandiri.
- Masa tenggang/naik air dihitung dengan zona waktu lokal yang konsisten, tahan terhadap restart, perubahan tanggal, dan pembukaan berulang. Jangan menaikkan air berulang kali untuk hari yang sama.
- Animasi bahtera/air menyesuaikan tema terang/gelap tetapi aturan matematika tidak berubah.

### 2.6 FULK Learn
**Landasan:** QS al-Mu’minūn [23]:27 — dipakai sebagai landasan konseptual terkait kisah Nabi Nuh/bahtera sesuai penelitian Barthes yang telah dilakukan. Jangan memperluasnya menjadi klaim bahwa ayat secara literal membahas literasi digital.
Fungsi:
- Materi pembelajaran tentang epistemic flooding, mengenali ancaman informasi dan manipulasi, serta menyiapkan respons sebelum ancaman berdampak.
- Modul wajib Smart Pause bernama `Mengenali Ancaman dan Manipulasi`.
- Modul memiliki materi yang jelas, contoh konkret, langkah respons sebelum bertindak, dan kuis pilihan ganda yang memadai (bukan hanya tiga soal); posisi jawaban benar harus bervariasi, tidak selalu opsi B.
- Tampilkan umpan balik untuk jawaban dan penjelasan mengapa jawaban benar/salah.
- Ketika masuk dari Smart Pause karena pengguna memilih melanjutkan, pembelajaran wajib diselesaikan dan tidak ada tombol `Lewati`. Jangan membuka jalan kembali ke media sosial sebelum pembelajaran dan evaluasi selesai sesuai alur yang disepakati.
- Materi video bahasa Indonesia diprioritaskan; video bahasa Inggris dengan subtitle dapat digunakan jika diperlukan. Penyimpanan offline video boleh memperbesar ukuran aplikasi sesuai keputusan terdahulu, tetapi gunakan lisensi/sumber yang sah dan dokumentasikan ukuran.
- Jangan menampilkan progres pelajaran selesai jika pengguna belum menyelesaikannya.

## 3. Layar landasan Qur’ani sebelum fitur
Setiap kali pengguna membuka salah satu dari enam fitur, tampilkan layar pengantar:
1. nama fitur;
2. teks Arab;
3. terjemahan Indonesia;
4. referensi surah/ayat;
5. penjelasan relevansi singkat dan tidak memaksakan tafsir;
6. tombol `Lanjutkan`.
Setelah itu masuk ke layar utama fitur. Ayat dan terjemahan harus diverifikasi dari sumber tepercaya sebelum rilis.

Pemetaan:
- Time: QS al-‘Aṣr [103]:1–3.
- Shield: QS al-Baqarah [2]:188.
- Check: QS al-Ḥujurāt [49]:6.
- Suara: QS al-Mā’idah [5]:2.
- Reflect: QS al-Ḥasyr [59]:18.
- Learn: QS al-Mu’minūn [23]:27.

## 4. Beranda dan navigasi
- Logo resmi pengguna: perisai biru-putih dengan simbol gelombang/bahtera putih; gunakan tanpa perubahan.
- Header gradasi biru dengan gelombang abstrak.
- Dua kartu ringkasan berdampingan.
- Enam fitur dalam grid tiga kolom × dua baris; gunakan layout adaptif bila perlu agar tetap mudah dibaca.
- Tidak ada bagian aktivitas tambahan di bawah grid pada desain beranda yang disepakati.
- Tema terang/gelap mengikuti sistem Android atau pilihan pengguna yang disimpan.
- Seluruh dialog, kartu, halaman, ikon, navigasi, dan ilustrasi harus menyesuaikan tema.
- Beranda modern minimalis dan hangat, tidak dipenuhi ornamen Qur’ani atau gambar kapal besar.
- Visual bahtera dan air khususnya menjadi ciri FULK Reflect.

## 5. Kualitas, privasi, dan definisi “berfungsi”
- Data harus tetap konsisten setelah aplikasi ditutup dan dibuka kembali.
- Penanganan offline/online harus jelas; mayoritas fitur dan materi membutuhkan internet sesuai keputusan pengguna.
- Permission onboarding untuk overlay, usage access, dan notifikasi harus transparan.
- Jangan meminta permission yang tidak dibutuhkan.
- Jangan mengirim data pribadi atau laporan tanpa persetujuan.
- Jangan memasukkan secrets/API keys ke repositori.
- Gunakan arsitektur yang bisa diuji: UI, domain/use-cases, repository/data source, provider adapters.
- Unit test untuk perhitungan Reflect, masa tenggang, bobot aktivitas, deduplikasi, dan batas notifikasi.
- UI/integration test untuk navigasi, layar Qur’ani, Smart Pause → Learn tanpa skip, mode tema, dan persistence.
- Build harus berhasil. Jika emulator/device tersedia, jalankan pengujian nyata. Laporkan yang sudah diuji dan yang belum, tanpa klaim palsu.
- Buat README dengan setup Codespaces, kebutuhan SDK/Gradle, variabel konfigurasi API, izin Android, dan keterbatasan platform.
- Jangan menyebut aplikasi selesai sebelum seluruh fungsi yang bisa diuji telah diuji; daftar integrasi eksternal yang masih membutuhkan kredensial/backend harus eksplisit.

## 6. Definisi selesai
Aplikasi dinyatakan siap uji ketika:
1. source project lengkap dan dapat dibangun;
2. semua layar utama dan enam layar pengantar Qur’ani berfungsi;
3. navigasi dan tema persisten;
4. alur Smart Pause → FULK Learn wajib tidak dapat dilewati;
5. aturan Reflect sesuai angka final dan teruji otomatis;
6. Check tidak menghasilkan verifikasi palsu;
7. Suara FULK tidak berpura-pura menjadi layanan komunitas/backend bila belum tersedia;
8. izin Android dan keterbatasannya didokumentasikan;
9. tes dan hasil build dilaporkan secara jujur.
