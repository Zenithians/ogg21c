# Topologi

Topologi OGG menggambarkan hubungan antara database source, proses replikasi, jaringan, dan database target.

## Topologi Umum

```text
[Source Database]
      |
  Extract
      |
 Local Trail
      |
 Data Pump / Distribution
      |
 Remote Trail
      |
  Replicat
      |
[Target Database]
```

## Pola Replikasi

| Pola | Deskripsi |
|---|---|
| Unidirectional | Replikasi satu arah dari source ke target. |
| Bidirectional | Dua database saling bertukar perubahan. |
| Hub and Spoke | Satu pusat data mendistribusikan perubahan ke beberapa target. |
| Cascading | Target dari satu replikasi menjadi source untuk replikasi berikutnya. |

Untuk dokumentasi ini, implementasi yang tersedia saat ini berfokus pada replikasi unidirectional.
