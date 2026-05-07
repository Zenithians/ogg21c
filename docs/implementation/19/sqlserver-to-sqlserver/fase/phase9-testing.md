# Testing Replikasi

## Test Dasar (INSERT, UPDATE, DELETE)

Jalankan DML berikut di database **PROD2** (Source):

```sql
USE PROD2;

-- INSERT
INSERT INTO dbo.employees (name, department, salary)
VALUES ('Andi', 'IT', 9000000);

-- UPDATE
UPDATE dbo.employees
SET salary = 9500000
WHERE name = 'Andi';

-- DELETE
DELETE FROM dbo.employees
WHERE name = 'Andi';
```

Kemudian cek hasilnya di **DRC** (Target):

```sql
USE DRC;
SELECT * FROM dbo.employees;
```

!!! success "Replikasi Berhasil"
    Jika data di DRC mencerminkan perubahan yang dilakukan di PROD2 secara real-time, maka replikasi berjalan dengan benar.

## Test Insert 1000 Data

Untuk menguji performa replikasi dengan volume data lebih besar, jalankan bulk insert di PROD2:

```sql
USE PROD2;

DECLARE @i INT = 1;
WHILE @i <= 1000
BEGIN
    INSERT INTO dbo.employees (name, department, salary)
    VALUES (
        CONCAT('Employee_', @i),
        CASE @i % 3
            WHEN 0 THEN 'IT'
            WHEN 1 THEN 'Finance'
            ELSE 'HR'
        END,
        5000000 + (@i * 1000)
    );
    SET @i = @i + 1;
END
```

## Verifikasi Jumlah Data

```sql
USE DRC;

-- Cek total data di Target
SELECT COUNT(*) AS total_target FROM dbo.employees;

-- Bandingkan Source dan Target
SELECT
    (SELECT COUNT(*) FROM PROD2.dbo.employees) AS source_count,
    (SELECT COUNT(*) FROM DRC.dbo.employees)   AS target_count;
```

!!! info "Catatan Replikasi"
    Data yang diinsert **sebelum** OGG dijalankan tidak akan ter-replikasi otomatis. OGG hanya mereplikasi perubahan yang terjadi setelah proses Extract aktif.

## Monitoring via GGSCI

Pantau status replikasi secara real-time:

```
-- Cek semua proses
GGSCI> INFO ALL

-- Cek statistik Extract
GGSCI> STATS EXTRACT ext1

-- Cek statistik Replicat
GGSCI> STATS REPLICAT rep1

-- Cek lag (keterlambatan replikasi)
GGSCI> LAG EXTRACT ext1
GGSCI> LAG REPLICAT rep1
```
