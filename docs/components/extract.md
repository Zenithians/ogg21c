# Extract

Extract adalah proses OGG yang menangkap perubahan data dari database source.

Pada database Oracle, Extract biasanya membaca redo log atau archive log. Pada database lain, mekanismenya mengikuti fitur capture yang didukung oleh database tersebut, misalnya transaction log atau CDC.

## Fungsi

- membaca perubahan `INSERT`, `UPDATE`, dan `DELETE`,
- menyaring object yang direplikasi,
- menulis perubahan ke local trail,
- menjaga posisi capture agar proses bisa dilanjutkan setelah restart.

## Output

Output utama Extract adalah trail file, yaitu file berisi data perubahan yang akan dikirim atau dibaca oleh proses berikutnya.
