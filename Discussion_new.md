# Hasil Diskusi Pertemuan 2

---

### 1. Bagaimana cara membedakan *attack surface* dan *attack vector*? Berikan contoh pada OJS!

Cara paling mudah membedakannya adalah dengan melihat konsep **"Di mana"** dan **"Bagaimana"**.

| Aspek | 🔵 Attack Surface (Permukaan Serangan) | 🔴 Attack Vector (Vektor Serangan) |
| :--- | :--- | :--- |
| **Definisi** | Titik masuk (*entry point*), antarmuka, atau fitur yang terekspos ke publik dan berpotensi diserang. | Cara, metode, atau teknik spesifik yang digunakan *attacker* untuk mengeksploitasi sistem. |
| **Fokus** | **"DI MANA sistem bisa diserang?"** (Lokasi) | **"BAGAIMANA cara menyerang sistem?"** (Aksi) |
| **Sifat** | Pasif (Sudah bagian dari sistem itu sendiri) | Aktif (Tindakan yang dilakukan oleh penyerang) |

**Contoh Kasus pada OJS:**
* **Attack Surface:** Halaman Login OJS (`/index.php/index/login`), Form Upload Submission, dan HTTP Response Headers.
* **Attack Vector:** Melakukan serangan *Brute-Force* ke halaman login, mengunggah *malware* via form submission, atau mengeksploitasi celah dari informasi server yang bocor di header.

---

### 2. Mengapa endpoint upload file (B1–B4) memiliki risiko lebih tinggi dibanding endpoint baca (GET)?

Endpoint *upload file* memiliki tingkat risiko (**Severity**) yang sangat tinggi karena fitur ini memberikan akses kepada pengguna untuk **menulis dan menyimpan file langsung ke dalam direktori server**. 

* **Risiko Upload File:** Jika sistem tidak memvalidasi jenis file dengan ketat (misalnya hanya mengecek ekstensi tanpa memvalidasi *MIME type* atau isi file), *attacker* bisa mengunggah *script* berbahaya seperti *PHP Web Shell*. Jika file ini berhasil diakses dan dieksekusi oleh server, dampaknya adalah **Remote Code Execution (RCE)**. *Attacker* bisa mengambil alih server secara penuh, memanipulasi *database*, hingga merusak sistem.
* **Perbandingan dengan Endpoint GET:** Endpoint baca (GET) umumnya hanya meminta (me-*retrieve*) data dari server. Walaupun bisa memiliki celah seperti *Information Disclosure* atau *Cross-Site Scripting* (XSS), sangat jarang dampaknya langsung berujung pada pengambilalihan server secara total seperti pada *file upload*.

---

### 3. Pada alur autentikasi OJS, di titik mana kemungkinan terbesar terjadinya SQL Injection? Jelaskan!

Kemungkinan terbesar terjadinya kerentanan *SQL Injection* (SQLi) berada pada **proses verifikasi kredensial di *Backend***, tepatnya saat memproses parameter input `username` dan `password` dari Form Login (*POST Request*).

**Penjelasan Alur Eksploitasi:**
Saat user memasukkan kredensial, *backend* akan merangkai input tersebut menjadi *query* ke *database*, contohnya: 
`SELECT * FROM users WHERE username = '$username' AND password = '$password'`

Jika OJS (terutama versi lama atau yang telah dimodifikasi) tidak menggunakan *Prepared Statements* (Parameterized Queries) atau tidak melakukan sanitasi terhadap input khusus (seperti tanda kutip `'`), *attacker* dapat memasukkan *payload* injeksi. 
Misalnya, memasukkan `admin' OR '1'='1` pada kolom *username*. *Query* akan berubah menjadi selalu *True* (benar), sehingga *attacker* berhasil melakukan *Bypass Authentication* dan masuk ke akun Admin tanpa perlu tahu *password* aslinya.

---

### 4. Sebutkan minimal 3 informasi sensitif yang mungkin bocor melalui HTTP response headers OJS!

Berdasarkan teknik *fingerprinting* (misalnya menggunakan *tools* WhatWeb pada PoC pengujian), *HTTP Response Headers* sering kali secara tidak sengaja membocorkan informasi sensitif yang mempermudah *attacker* menyusun strategi serangan (*Information Disclosure*). 

Berikut 3 informasi yang paling sering bocor:
1. **Versi Web Server Secara Detail:** (Contoh: `Server: Apache/2.4.58`). Informasi ini memungkinkan *attacker* untuk langsung mencari *exploit* publik (CVE) yang secara spesifik menargetkan versi Apache tersebut.
2. **Sistem Operasi (OS) yang Berjalan:** (Contoh: `(Ubuntu)` yang terlampir pada header server). Memberitahu *attacker* tentang arsitektur *environment* target, sehingga mereka tahu jenis *payload* apa yang cocok.
3. **Teknologi Backend/Framework yang Digunakan:** (Contoh: `X-Powered-By: PHP/8.1`). Menunjukkan bahasa pemrograman yang digunakan, atau kebocoran nama *cookies* spesifik seperti `OJSSID` yang bisa dieksploitasi untuk serangan pembajakan sesi (*Session Hijacking*).
