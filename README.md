1. Mengapa memilih konfigurasi col tertentu untuk tiap breakpoint?
Saya memilih konfigurasi col (column) ini karena prinsipnya mengikuti DNA asli Instagram dan kebutuhan visual developer:

* Default (Mobile / <576px): col-12
  
- Kenapa? Agar postingan menjadi satu kolom penuh. Di HP, kita kan biasanya scroll vertikal. Ini paling optimal untuk pengalaman melihat konten di layar kecil.

*Medium/Large (Desktop / ≥768px): col-4 (Grid 3 Kolom)

-Ini adalah konfigurasi mutlak yang meniru tampilan standar Instagram versi desktop. Semua postingan harus tampil dalam 3 kolom yang sama lebar. Kenapa? Karena itu adalah ciri khas paling ikonik dari tampilan feed profil Instagram. Intinya, agar mirip aslinya!

2. Bagaimana Anda memastikan tombol "Follow/Edit Profile" tetap mudah dijangkau di mobile? Jelaskan pendekatannya.
Pendekatan yang saya pakai adalah Hierarki dan Re-ordering dengan Flexbox/Media Query:

* Prioritas di HTML: Secara markup (di index.html), tombol Follow/Edit Profile saya letakkan di dekat nama pengguna (username). Ini penting karena secara default, tombol ini harus terlihat jelas.

* Mobile (Saat Breakpoint Aktif):

-Saya menggunakan Media Query untuk breakpoint kecil.

-Tombol ini saya paksa untuk mengambil lebar penuh (width: 100%; atau flex-basis: 100%;), dan saya beri margin atau padding vertikal.

-Dengan Flexbox, saya bisa menggunakan properti flex-wrap: wrap; pada container profil. Jadi, ketika tombol itu full-width, dia otomatis turun ke baris baru di bawah profile info tanpa mengganggu layout foto profil dan bio.

-Intinya: Di mobile, tombol ini menjadi elemen tunggal yang full-width di bawah info utama profil, membuatnya besar, mudah diklik, dan tidak perlu scroll ekstra untuk menemukannya.

3. Jika postingan bertambah jadi 50, apa potensi masalah dan bagaimana solusi grid Anda mengatasinya?

* Potensi Masalah (Saat Postingan 50):
Masalah terbesarnya bukan pada layout-nya, tetapi pada Performa dan User Experience (UX).

-Performa (Loading Berat): 50 gambar resolusi tinggi yang di-load sekaligus (apalagi dengan thumbnail di grid) bakal bikin page menjadi berat dan lama banget di-load. Ini bisa membuat pengguna kabur.

-Scrolling Jauh: Pengguna harus scroll sangat jauh untuk melihat footer atau postingan lama, padahal kebanyakan pengguna hanya peduli pada 10-20 postingan terakhir.

* Solusi Grid Saya untuk Mengatasinya:
Grid CSS/Flexbox yang saya buat sebenarnya sangat stabil untuk menangani 50 item (dia otomatis membentuk 3 kolom dan terus berlanjut ke bawah). Namun, agar solusinya lebih realistis dan efisien (seperti Instagram asli), saya akan mengadopsi dua teknik:

* Prioritas (Solusi Cepat): Lazy Loading (di luar lingkup HTML/CSS)

-Secara markup, saya akan menerapkan atribut loading="lazy" pada tag <img> di postingan-postingan yang berada di luar viewport awal (below the fold).

-Ini memastikan hanya 12-15 gambar pertama yang dimuat saat page load. Gambar sisanya akan di-load hanya saat pengguna mulai scroll ke bawah. Performa menjadi lebih ringan.

* Solusi Jangka Panjang: Pagination atau Infinite Scrolling

-Jika ini adalah proyek full-stack, saya tidak akan menampilkan 50 postingan sekaligus.

-Akan ada pembatasan (misalnya, hanya 24 postingan per load).

-Saya akan menggunakan JavaScript untuk menerapkan Infinite Scrolling: Grid akan dibuat hanya untuk 24 postingan, dan ketika pengguna mencapai bagian bawah halaman, JS akan memicu request data baru, dan menambahkan 24 item berikutnya ke grid yang sudah ada.
