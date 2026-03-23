
## A. REST API Entry Points (OJS)

| Endpoint | Method | Deskripsi | Risiko |
|----------|--------|----------|--------|
| /api/v1/users | GET | Mengambil daftar user | Information Disclosure, IDOR |
| /api/v1/submissions | GET/POST | Mengelola submission | IDOR, Unauthorized Access |
| /api/v1/contexts | GET | Data jurnal | Information Disclosure |
| /api | GET | Root API endpoint | API enumeration |

## B. Admin Entry Points

| Endpoint | Method | Deskripsi | Risiko |
|----------|--------|----------|--------|
| /index.php/index/admin | GET | Dashboard admin | Unauthorized access |
| /index.php/index/admin/plugins | GET/POST | Manajemen plugin | RCE |
| /index.php/index/admin/users | GET/POST | Manajemen user | Privilege escalation |
| /index.php/index/admin/settings | POST | Konfigurasi sistem | SSRF, misconfig |
