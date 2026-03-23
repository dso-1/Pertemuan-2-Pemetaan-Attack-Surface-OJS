# Recon Summary — 10.34.100.178

## Target Information

| Field        | Value                          |
|--------------|-------------------------------|
| IP Address   | 10.34.100.178                 |
| OS           | Ubuntu Linux                  |
| Web Server   | Apache 2.4.58 (Ubuntu)        |
| CMS          | Open Journal Systems 3.3.0.8  |
| Country      | RESERVED (Internal Network)   |

## Open Ports

| Port | State | Service | Version                              |
|------|-------|---------|--------------------------------------|
| 22   | open  | SSH     | OpenSSH 9.6p1 Ubuntu 3ubuntu13.15   |
| 80   | open  | HTTP    | Apache httpd 2.4.58 (Ubuntu)        |

## Discovered Paths (Gobuster + ffuf)

| Path           | Status | Notes                    |
|----------------|--------|--------------------------|
| /index.php     | 200    | Main OJS entry point     |
| /api/          | 301    | OJS REST API             |
| /cache/        | 301    | Disallowed in robots.txt |
| /classes/      | 301    | OJS classes directory    |
| /controllers/  | 301    | OJS controllers          |
| /docs/         | 301    | Documentation            |
| /javascript/   | 301    | JavaScript files         |
| /js/           | 301    | JS directory             |
| /lib/          | 301    | Libraries                |
| /locale/       | 301    | Language files           |
| /pages/        | 301    | OJS pages                |
| /plugins/      | 301    | Installed plugins        |
| /public/       | 301    | Public assets            |
| /schemas/      | 301    | Schemas                  |
| /styles/       | 301    | CSS styles               |
| /templates/    | 301    | OJS templates            |
| /tools/        | 301    | OJS tools                |
| /robots.txt    | 200    | Disallows /cache/        |
| /favicon.ico   | 200    | Favicon                  |
| /.htaccess     | 403    | Forbidden                |
| /.htpasswd     | 403    | Forbidden                |
| /server-status | 403    | Apache mod_status        |

## Technologies Detected (WhatWeb)

| Technology  | Value                        |
|-------------|------------------------------|
| Framework   | Bootstrap                    |
| JavaScript  | jQuery                       |
| Cookie      | OJSSID                       |
| HTML        | HTML5                        |
| Generator   | Open Journal Systems 3.3.0.8 |

## Output Files

| File                 | Tool      | Description              |
|----------------------|-----------|--------------------------|
| whatweb_output.txt   | WhatWeb   | Fingerprinting results   |
| nmap_scan.txt        | Nmap      | Port scan results        |
| gobuster_output.txt  | Gobuster  | Directory enumeration    |
| ffuf_output.json     | ffuf      | Directory fuzzing        |
| recon_summary.md     | Manual    | This summary file        |
EOF
