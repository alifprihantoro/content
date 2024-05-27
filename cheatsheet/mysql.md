## user management
```sql
-- created
CREATE USER 'eko'@'localhost';
CREATE USER 'khannedy'@'%';
-- delete user
DROP USER 'eko'@'localhost';
DROP USER 'khannedy'@'%';

-- give grant
GRANT SELECT ON belajar_mysql.* TO 'eko'@'localhost';

GRANT SELECT ON belajar_mysql.* TO 'khannedy'@'%';
GRANT INSERT, UPDATE, DELETE ON belajar_mysql.* TO 'khannedy'@'%';

-- check grants user
SHOW GRANTS FOR 'eko'@'localhost';
SHOW GRANTS FOR 'khannedy'@'%';

-- set passiword
SET PASSWORD FOR 'eko'@'localhost' = 'rahasia';
SET PASSWORD FOR 'khannedy'@'%' = 'rahasia';
```

## types

1. **String Data Types**:

   - **CHAR (size)**: String dengan panjang tetap (dapat berisi huruf, angka, dan karakter khusus). Parameter `size` menentukan panjang kolom dalam karakter (0 hingga 255). Nilai default adalah 1.
   - **VARCHAR (size)**: String dengan panjang variabel (dapat berisi huruf, angka, dan karakter khusus). Parameter `size` menentukan panjang maksimum kolom dalam karakter (0 hingga 65535).
   - **BINARY (size)**: Sama dengan **CHAR**, tetapi menyimpan string byte biner. Parameter `size` menentukan panjang kolom dalam byte. Nilai default adalah 1.
   - **VARBINARY (size)**: Sama dengan **VARCHAR**, tetapi menyimpan string byte biner. Parameter `size` menentukan panjang maksimum kolom dalam byte.
   - **ENUM (val1, val2, val3, ...)**: Objek string yang hanya dapat memiliki satu nilai, dipilih dari daftar nilai yang mungkin. Anda dapat menyebutkan hingga 65535 nilai dalam daftar ENUM. Jika nilai yang dimasukkan tidak ada dalam daftar, akan dimasukkan nilai kosong. Nilai diurutkan sesuai urutan yang Anda masukkan.
   - **SET (val1, val2, val3, ...)**: Objek string yang dapat memiliki 0 atau lebih nilai, dipilih dari daftar nilai yang mungkin. Anda dapat menyebutkan hingga 64 nilai dalam daftar SET.

2. **Numeric Data Types**:

   - **BIT (size)**: Tipe nilai bit. Jumlah bit per nilai ditentukan oleh `size`. Parameter `size` dapat bernilai 1 hingga 64. Nilai default untuk `size` adalah 1.
   - **TINYINT (size)**: Integer sangat kecil. Rentang nilai dengan tanda adalah -128 hingga 127. Rentang tanpa tanda adalah 0 hingga 255. Parameter `size` menentukan lebar tampilan maksimum (yang adalah 255).
   - **BOOL**: Nol dianggap sebagai **false**, nilai selain nol dianggap sebagai **true**.
   - **BOOLEAN**: Sama dengan **BOOL**.
   - **SMALLINT (size)**: Integer kecil. Rentang dengan tanda adalah -32768 hingga 32767. Rentang tanpa tanda adalah 0 hingga 65535. Parameter `size` menentukan lebar tampilan maksimum (yang adalah 255).
   - **MEDIUMINT (size)**: Integer sedang. Rentang dengan tanda adalah -8388608 hingga 8388607.

3. **Date and Time Data Types**:
   - MySQL mendukung tipe data tanggal dan waktu seperti **DATE**, **TIME**, **DATETIME**, dan **TIMESTAMP**.

## manage table

```sql
SHOW ENGINES;

SHOW TABLES;

CREATE TABLE barang
(
    id     INT          NOT NULL,
    nama   VARCHAR(100) NOT NULL,
    harga  INT          NOT NULL DEFAULT 0,
    jumlah INT          NOT NULL DEFAULT 0
) ENGINE = InnoDB;

DESCRIBE barang;

SHOW CREATE TABLE barang;

ALTER TABLE barang
    ADD COLUMN deskripsi TEXT;

ALTER TABLE barang
    ADD COLUMN salah TEXT;

ALTER TABLE barang
    DROP COLUMN salah;

ALTER TABLE barang
    MODIFY nama VARCHAR(200) AFTER deskripsi;

ALTER TABLE barang
    MODIFY nama VARCHAR(200) FIRST;

ALTER TABLE barang
    MODIFY id INT NOT NULL;

ALTER TABLE barang
    MODIFY nama VARCHAR(200) NOT NULL;

SHOW CREATE TABLE barang;

ALTER TABLE barang
    MODIFY jumlah INT NOT NULL DEFAULT 0;

ALTER TABLE barang
    MODIFY harga INT NOT NULL DEFAULT 0;

ALTER TABLE barang
    ADD waktu_dibuat TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP;

INSERT INTO barang (id, nama)
VALUES (1, 'Apel');

SELECT *
FROM barang;

TRUNCATE barang;

SHOW tables;

DROP TABLE barang;
```

## CRUD table
### create
```sql
CREATE TABLE `users` (
  `uid` INT AUTO_INCREMENT PRIMARY KEY,
  `username` VARCHAR(50) NOT NULL,
  `passwd` VARCHAR(255) NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  `verified` BOOLEAN NOT NULL DEFAULT FALSE
);

INSERT INTO `users` (`username`, `passwd`, `email`, `uid`, `verified`)
VALUES
  ('user1', 'password1', 'user1@example.com', FLOOR(RAND() * 1000), TRUE),
  ('user2', 'password2', 'user2@example.com', FLOOR(RAND() * 1000)),
  -- Tambahkan 8 baris data lainnya dengan cara yang sama
  ('user10', 'password10', 'user10@example.com', FLOOR(RAND() * 1000));

CREATE TABLE `user_post` (
  `slug` VARCHAR(100) PRIMARY KEY,
  `title` VARCHAR(255) NOT NULL,
  `content` TEXT NOT NULL,
  `uid` INT NOT NULL,
  `publish` BOOLEAN DEFAULT FALSE,
  `lastupdate` TIMESTAMP DEFAULT NOW(),
  `publish` TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY (`uid`) REFERENCES `users`(`id`) ON DELETE CASCADE
);

-- create trigger
DELIMITER //
CREATE TRIGGER update_lastpublish
BEFORE INSERT ON user_post
FOR EACH ROW
BEGIN
    SET NEW.lastpublish = NOW();
END;
//
DELIMITER ;

INSERT INTO `user_post` (`slug`, `title`, `content`, `uid`)
VALUES
  ('user1/post-1', 'Judul Postingan 1', 'Isi postingan 1...', 1),
  ('user2/post-1', 'Judul Postingan 1', 'Isi postingan 1...', 1),
  ('user1/post-2', 'Judul Postingan 2', 'Isi postingan 2...', 2),
  ('user1/post-10', 'Judul Postingan 10', 'Isi postingan 10...', 3);
  -- tidak bisa sama jika username sama
  ('user1/post-1', 'Judul Postingan 1', 'Isi postingan 1...', 1),
```
### get and search
```sql
-- get list post by uid
SELECT title, slug
FROM user_post
WHERE uid = 1;

-- search by title
SELECT title, slug
FROM user_post
WHERE title LIKE '%kata_kunci%';

-- search by title or slug
SELECT title, slug
FROM user_post
WHERE title LIKE '%kata_kunci%'
   OR slug LIKE '%kata_kunci%';
```

### update
```sql
UPDATE user_post
SET title = 'Judul Baru', slug = 'slug-baru'
WHERE uid = 1;
```

### delete
```sql
DELETE FROM user_post
WHERE slug = 'user1/post-1';
`DELIMITER //
CREATE TRIGGER update_lastpublish
BEFORE INSERT ON my_content
FOR EACH ROW
BEGIN
    SET NEW.lastpublish = NOW();
END;
//
DELIMITER ;
``