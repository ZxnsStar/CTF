head-dump

Kategori: Web Exploitation

Tingkat Kesulitan: Easy

Poin: -

Platform: CyLab Security Academy

Tanggal Selesai: Kamis, 8 Oktoer 2026

📌 Deskripsi Challenge

Deskripsi: Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.

The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.

Lampiran File / Target IP: http://chatelaine.cylabacademy.net:28820/ dan heapdump-1791415867974.heapsnapshot

🔍 Analisis Awal (Reconnaissance)

Pemindaian / Pengumpulan Informasi:

Pada tampilan halaman pertama website, terdapat satu card yang menarik perhatian yaitu link yang bertuliskan #API Documentation.
Link ini akan me-redirect user ke file api documentation.html .
Di dalam website tersebut terdapat beberapa menu API endpoints yang bisa kita gunakan dan kita inspeksi lebih lanjut.
Bagian Diagnosing tepatnya di /heapdump API endpoint, kita bisa mencoba dengan meng-klik pada tombol 'Try it out!' hingga muncul tombol execute dan klik tombol execute.
Ketika selesai diexecute, api tersebut akan menghasilkan suatu output/response dari server dimana kita bisa mendownload sebuah file dengan ekstensi .heapsnapshot .
setelah file didownload, maka kita bisa mencari atau menginspeksi isi dari file tersebut dengan menggunakan cli (disini saya menggunakan cli dari archlinux), dan menuliskan command berikut ( cp /mnt/c/Users/Lenovo/Downloads/heapdump-1791415867974.heapsnapshot . ) command ini berfungsi untuk meng-copy file dari direktori pc ke direktori aktif pada cli yang dipakai.
Kemudian setelah kita copy file, kita bisa mulai inspeksi file dengan command ( cat heapdump-1791415867974.heapsnapshot | fold -s -w 100 | grep -i "academy" ) sehingga kita menemukan key/flag nya academy{...} .


Temuan Awal:

Ditemukan link yang tercantum pada post card disebuah 'akun' dari PicoCTF, link tersebut akan mengarahkan ke API Documentation yang dipakai oleh website tersebut.

Ditemukan endpoint /heapdump pada link API Documentation sebelumnya.

🛠️ Langkah Eksploitasi / Penyelesaian (Walkthrough)

Langkah 1: Klik link #API Documentation pada post card swagger.

Ketika link tersebut di-klik, akan me-redirect ke halaman API Documentation dari swagger yang akan memperlihatkan rute API yang bisa digunakan.

Langkah 2: Cari endpoint yang mencurigakan.

Dari langkah sebelumnya, kita bisa mencari mana endpoint yang mencurigakan dan saya memilih endpoint /heapdump. Kenapa saya memilih endpoint /heapdump? Karena deskripsi endpoint ini sama dengan hint challenge sehingga saya bisa yakin bahwa endpoint inilah yang memang benar untuk dibedah lebih lanjut.
Pada endpoint tersebut klik tombol "Try it out". Kemudian tombol "execute" akan muncul, maka tekan tombol "execute" tersebut.
Setelah proses execute selesai maka akan menghasilkan response dari server.

Langkah 3: Download file dan pindah file dari direktori windows ke direktori aktif cli archlinuxnya.

Download link yang ada pada response dari langkah sebelumnya dengan ekstensi .heapdump .
Setelah file terdownload, maka copy file tersebut ke dari direktori windows ke direktori aktif cli archlinux dengan command:( cp /mnt/c/Users/Lenovo/Downloads/heapdump-1791415867974.heapsnapshot . )

Langkah 4: Mencari flag di dalam file .heapdump [Penyelesaian]

File .heapdump yang telah selesai di salin ke direktori aktif cli, kita inspeksi isinya dengan menggunakan command:( cat heapdump-1791415867974.heapsnapshot | fold -s -w 100 | grep -i "academy" )

Screenshot / Catatan:

Disini saya menggunakan alat/software bantuan yaitu command line interface dari Archlinux.

<img width="1896" height="970" alt="Screenshot 2026-10-08 065506" src="https://github.com/user-attachments/assets/1a3d417b-ace4-4ca2-aed1-4f9cefd85d4e" /> Gambar 1. Tampilan awal website swagger
<img width="1896" height="727" alt="Screenshot 2026-10-08 070202" src="https://github.com/user-attachments/assets/2032aa05-ac23-4584-b3d6-18c07bebf3b7" /> Gambar 2. Endpoint /heapdump
<img width="1886" height="890" alt="Screenshot 2026-10-08 070215" src="https://github.com/user-attachments/assets/c5eb501b-d298-41d1-91ac-e61e7793a9ec" /> Gambar 3. Response dari server


🚩 Flag

Tuliskan format flag akhir yang berhasil Anda dapatkan.

academy{Pat!3nt_15_Th3_K3y_cc0f4fda}

💡 Pelajaran & Dampak Keamanan (Remediation / Mitigation)

Jelaskan analisis keamanan dan cara memperbaiki celah tersebut dari sudut pandang defensif.

Penyebab Kerentanan: Mengapa tantangan ini bisa dieksploitasi? (contoh: Sanitasi input yang kurang lengkap pada form login).

Solusi / Perbaikan (Remediation):

Gunakan Parameterized Queries atau Prepared Statements untuk mencegah SQL Injection.

Terapkan sanitasi dan validasi input yang ketat pada sisi server.

🔗 Referensi

Link Dokumentasi / Artikel Terkait

Cheat Sheet Terkait
