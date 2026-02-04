# Landing Page - Instruksi Menambahkan Foto

## Cara Menambahkan Foto Hero

1. Simpan foto Anda dengan nama `hero-image.jpg` di folder **public**:
   ```
   /public/hero-image.jpg
   ```

2. Format foto yang disarankan:
   - Format: JPG, PNG, atau WebP
   - Ukuran: Minimal 800x1000px (rasio 3:4 atau 4:5)
   - Ukuran file: Maksimal 2MB untuk performa optimal

3. Jika foto tidak ditemukan, akan muncul placeholder default.

## Alternatif: Menggunakan URL Eksternal

Jika ingin menggunakan foto dari URL eksternal, edit file `LandingPage.svelte` dan ubah:
```svelte
src="/hero-image.jpg"
```
menjadi:
```svelte
src="https://your-image-url.com/image.jpg"
```

## Catatan

- File di folder `public` dapat diakses langsung dengan path `/nama-file.jpg`
- Pastikan nama file sesuai dengan yang ada di kode (hero-image.jpg)
