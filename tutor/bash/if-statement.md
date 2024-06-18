## bassic if statement

- Untuk **sama dengan** (equivalent to `===` in JS), gunakan `-eq` untuk angka atau `==` untuk string.
- Untuk **kurang dari atau sama dengan** (`<=`), gunakan `-le`.
- Untuk **kurang dari** (`<`), gunakan `-lt`.
- Untuk **lebih besar dari atau sama dengan** (`>=`), gunakan `-ge`.
- Untuk **lebih besar dari** (`>`), gunakan `-gt`.
- Untuk **tidak sama dengan** (`!=`), gunakan `-ne` untuk angka atau `!=` untuk string.

Contoh penggunaan dalam skrip bash:

```bash
if [ "$a" -eq "$b" ]; then
  echo "a sama dengan b"
fi

if [ "$a" -le "$b" ]; then
  echo "a kurang dari atau sama dengan b"
fi

# dan seterusnya...
```

> [!IMPORTANT]
> Perhatikan bahwa untuk perbandingan string, kita menggunakan `==` dan `!=`. Apakah ada hal lain yang bisa saya bantu?

### Untuk **jika string cocok dengan string** (string matches):

```bash
if [ "$string1" == "$string2" ]; then
  echo "String cocok."
fi
```

### Untuk **jika string tidak cocok dengan string** (string does not match):

```bash
if [ "$string1" != "$string2" ]; then
  echo "String tidak cocok."
fi
```

### regex

Untuk menggunakan regex dalam kondisi `if` di bash, Anda bisa menggunakan operator `=~`. Berikut adalah contoh penggunaannya dengan regex:

```bash
string="foo soeme random bar"
if [[ "$string" =~ ^foo.*bar$ ]]; then
  echo "String cocok dengan regex."
fi
```

Dalam contoh ini, `^foo.*bar$` adalah regex yang memeriksa apakah string diawali dengan 'foo', diikuti oleh karakter apa pun (dinyatakan dengan `.*`), dan diakhiri dengan 'bar'. Apakah ada pola regex tertentu yang ingin Anda gunakan?
Perlu diingat bahwa spasi di sekitar tanda kurung siku `[ ]` sangat penting di bash. Apakah ada contoh khusus yang ingin Anda lihat?

### regex not

Untuk menggunakan negasi dengan regex dalam kondisi `if` di bash, Anda bisa menambahkan `!` sebelum operator `=~`. Berikut adalah contoh penggunaannya:

```bash
string="fsdalhf"
if [[ ! "$string" =~ ^foo.*bar$ ]]; then
  echo "String tidak cocok dengan regex."
fi
```

Dalam contoh ini, kita memeriksa bahwa string **tidak** cocok dengan pola regex yang diberikan. Apakah ini membantu?

### match in array
see in [here](./array.md#contains-var)