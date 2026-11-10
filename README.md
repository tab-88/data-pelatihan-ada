# Pusat Data Pelatihan Analis Data Muda

Situs statis untuk alamat `https://data-pelatihan-ada.promath.site`. Tidak ada proses build dan tidak ada kunci rahasia di dalamnya, sehingga seluruh isi folder ini aman disimpan di repositori GitHub publik.

## Isi folder

| Berkas | Fungsi |
| --- | --- |
| `index.html` | Halaman utama: tabel transaksi 505 baris x 14 kolom (`id="tabel-transaksi"`) dan kamus data, untuk latihan scraping (Sesi 3) |
| `daftar_produk.html` | Tabel produk dan wilayah untuk latihan Beautiful Soup (Sesi 3) |
| `robots.txt` | Contoh aturan pengambilan data untuk latihan etika (folder `/privat/` tidak boleh diambil) |
| `style.css` | Tampilan kedua halaman |

Berkas CSV tidak disimpan di folder ini dan tidak ditautkan dari situs. CSV tetap berada di Google Drive sebagai pintu data yang terpisah, supaya latihan scraping tidak punya jalan pintas.

## Langkah 1. Periksa di VS Code

Buka folder ini di VS Code (File, Open Folder). Pasang ekstensi Live Server bila belum ada, klik kanan `index.html`, lalu pilih Open with Live Server. Pastikan kedua halaman tampil dan tautannya berpindah dengan benar.

## Langkah 2. Kirim ke GitHub

Buat repositori kosong di GitHub dengan nama `data-pelatihan-ada`, lalu jalankan perintah berikut dari terminal VS Code di dalam folder ini.

```bash
git init
git add .
git commit -m "Situs data pelatihan"
git branch -M main
git remote add origin https://github.com/NAMA-AKUN-ANDA/data-pelatihan-ada.git
git push -u origin main
```

Ganti `NAMA-AKUN-ANDA` dengan nama pengguna GitHub Prof.

## Langkah 3. Terbitkan di Vercel

1. Masuk ke vercel.com dengan akun GitHub, pilih Add New, lalu Project.
2. Pilih repositori `data-pelatihan-ada` dan klik Import.
3. Pada Framework Preset pilih Other. Kosongkan Build Command dan Output Directory, karena situs ini murni HTML.
4. Klik Deploy. Vercel memberi alamat sementara berakhiran `.vercel.app`, dan alamat itu sudah dapat dibuka.

## Langkah 4. Pasang subdomain

1. Di proyek Vercel, buka Settings, lalu Domains, dan tambahkan `data-pelatihan-ada.promath.site`.
2. Vercel menampilkan satu catatan DNS bertipe CNAME. Buka pengelola DNS domain `promath.site`, buat catatan CNAME dengan nama `data-pelatihan-ada`, dan isi nilainya persis seperti yang ditampilkan Vercel. Nilai itu khusus untuk proyek Prof dan bentuknya mirip `xxxxxxxxxxxx.vercel-dns-017.com`, jadi salin dari layar Vercel dan jangan menebaknya.
3. Tunggu sampai status domain di Vercel berubah menjadi Valid Configuration. Sertifikat HTTPS dipasang otomatis.

## Langkah 5. Uji sebelum dipakai

Buka tiga alamat berikut dari jaringan lain (misalnya data seluler): halaman utama, `/daftar_produk.html`, dan `/robots.txt`. Setelah itu uji dari Google Colab memakai akun yang bukan akun Prof.

```python
import pandas as pd, requests
from bs4 import BeautifulSoup

# 1. CSV dari Google Drive
df = pd.read_csv("https://drive.google.com/uc?export=download&id=1XudocGK4kEDIYAKepW8g2o7UKrIZrgC8")
print(df.shape)                       # harus (505, 14)

# 2. Tabel produk dari situs
html = requests.get("https://data-pelatihan-ada.promath.site/daftar_produk.html").text
tabel = BeautifulSoup(html, "html.parser").find("table", id="tabel-produk")
print(len(tabel.tbody.find_all("tr")))  # harus 22
```

Syarat agar langkah pertama berhasil: pengaturan berbagi berkas CSV di Google Drive harus Anyone with the link, dengan peran Viewer.

## Mengubah isi situs

Ubah berkas di VS Code, lalu jalankan `git add .`, `git commit -m "pesan"`, dan `git push`. Vercel menerbitkan ulang otomatis dalam beberapa detik.
