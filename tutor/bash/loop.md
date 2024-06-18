## Untuk **folder**:
```bash
for folder in */ ; do
  echo "Folder: $folder"
done
```

## Untuk **file**:
```bash
for file in * ; do
  if [ -f "$file" ]; then
    echo "File: $file"
  fi
done
```

Dalam contoh pertama, loop `for` mengiterasi semua folder di direktori saat ini. Dalam contoh kedua, loop `for` mengiterasi semua item dan menggunakan kondisi `if` untuk memeriksa apakah item tersebut adalah file sebelum mencetak namanya. Apakah ada yang spesifik yang Anda cari dalam loop ini?

## loop array
check [here](./array.md#loop)