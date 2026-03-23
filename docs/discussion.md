# Jawaban Pertanyaan Diskusi

**1. Perbedaan Attack Surface dan Attack Vector pada OJS:**
* **Attack Surface:** Total titik di mana penyerang bisa berinteraksi, contoh: halaman login OJS.
* **Attack Vector:** Metode untuk mengeksploitasi titik tersebut, contoh: SQL Injection pada input username.

**2. Risiko Endpoint Upload (B1-B4) vs Read (GET):**
Endpoint upload memiliki risiko lebih tinggi karena memungkinkan penyerang menempatkan file eksekusi (seperti web shell PHP) langsung ke sistem file server, yang dapat berujung pada pengambilalihan server (RCE).

**3. Titik SQL Injection pada Autentikasi:**
Kemungkinan terbesar terjadi pada fungsi `UserDAO::getByUsername($username)` jika input tidak disanitasi sebelum dieksekusi ke database.

**4. Informasi Sensitif pada HTTP Response Header:**
- Versi server (Contoh: `Apache/2.4.58 (Ubuntu)`).
- Versi CMS (Contoh: `OJS 3.3.0.8`).
- Teknologi backend (Contoh: `PHP/7.4.33`).
