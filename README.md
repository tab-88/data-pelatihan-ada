# Data Pelatihan Analis Data Muda

Situs statis untuk alamat `https://data-pelatihan-ada.promath.site`. Isinya berupa laporan dalam bentuk tabel HTML yang diambil peserta dengan scraping pada Sesi 3.

| Berkas | Isi |
| --- | --- |
| `index.html` | Laporan penjualan: tabel `tabel-transaksi`, 505 baris x 14 kolom, data mentah |
| `daftar_produk.html` | Tabel `tabel-produk` (22 baris) dan `tabel-wilayah` (6 baris) |
| `robots.txt` | Aturan pengambilan data untuk latihan etika (`/privat/` tidak boleh diambil) |
| `style.css` | Tampilan |

CSV tidak disimpan di sini dan tidak ditautkan dari situs. CSV berada di Google Drive sebagai pintu data yang terpisah.

## Menerbitkan

1. Buka folder ini di VS Code, jalankan Live Server pada `index.html`, lalu periksa tampilannya.
2. Jalankan `git add -A`, `git commit -m "pesan"`, dan `git push` ke repositori GitHub.
3. Vercel menerbitkan ulang otomatis setiap ada push (Framework Preset Other, tanpa build).
4. Subdomain: tambahkan `data-pelatihan-ada.promath.site` di Vercel (Settings, Domains), lalu buat catatan CNAME di DNS `promath.site` dengan nilai persis seperti yang ditampilkan Vercel.
