# sed in bash
```bash
echo "Hello World" | sed 's/World/Linux/'
```

Perintah ini akan mengganti kata "World" dengan "Linux" dalam string "Hello World", sehingga outputnya akan menjadi "Hello Linux".

Apakah ada kasus penggunaan khusus yang ingin Anda ketahui?

## Contoh regex
- `*` (nol atau lebih dari karakter sebelumnya):
  ```bash
  echo "baaaat" | sed 's/ba*/b/'
  ```
  Output: `bt` (mencocokkan "ba" diikuti oleh nol atau lebih "a")

- `\+` (satu atau lebih dari karakter sebelumnya):
  ```bash
  echo "baaaat" | sed 's/ba\+/b/'
  ```
  Output: `bt` (mencocokkan "ba" diikuti oleh satu atau lebih "a")

- `\?` (nol atau satu dari karakter sebelumnya):
  ```bash
  echo "bat" | sed 's/ba\?/b/'
  ```
  Output: `bt` (mencocokkan "b" diikuti oleh nol atau satu "a")

- `\{i\}` (tepat i jumlah dari karakter sebelumnya):
  ```bash
  echo "baaaat" | sed 's/a\{3\}/x/'
  ```
  Output: `baxt` (mengganti tepat tiga "a" dengan "x")

- `\{i,j\}` (antara i dan j jumlah dari karakter sebelumnya):
  ```bash
  echo "baaaat" | sed 's/a\{2,3\}/x/'
  ```
  Output: `baxt` (mengganti antara dua dan tiga "a" dengan "x")

- `\{i,\}` (lebih dari atau sama dengan i jumlah dari karakter sebelumnya):
  ```bash
  echo "baaaat" | sed 's/a\{2,\}/x/'
  ```
  Output: `bxt` (mengganti dua atau lebih "a" dengan "x")

- `\(regexp\)` (grup):
  ```bash
  echo "ababab" | sed 's/\(ab\)\{2\}/x/'
  ```
  Output: `xab` (mengganti dua urutan "ab" dengan "x")

- `.` (cocok dengan karakter apapun):
  ```bash
  echo "bat" | sed 's/.at/x/'
  ```
  Output: `x` (mengganti "bat" dengan "x", karena "." cocok dengan karakter apapun)

- `^` (awal dari string):
  ```bash
  echo "start here" | sed 's/^start/finish/'
  ```
  Output: `finish here` (mengganti kata yang berada di awal string)

- `$` (akhir dari string):
  ```bash
  echo "end here" | sed 's/here$/there/'
  ```
  Output: `end there` (mengganti kata yang berada di akhir string)

- `[list]` (cocok dengan karakter apapun dalam list):
  ```bash
  echo "hat" | sed 's/[aeiou]/o/'
  ```
  Output: `hot` (mengganti vokal pertama dengan "o")

- `[^list]` (cocok dengan karakter apapun tidak dalam list):
   ```bash
   echo "hat" | sed 's/[^aeiou]/c/'
   ```
   Output: `cat` (mengganti konsonan pertama dengan "c")

- `regexp1\|regexp2` (cocok dengan regexp1 atau regexp2):
   ```bash
   echo "bat or cat" | sed 's/bat\|cat/rat/'
   ```
   Output: `rat or rat` (mengganti "bat" atau "cat" dengan "rat")

- `regexp1regexp2` (konkatenasi regexp1 dan regexp2):
   ```bash
   echo "abcde" | sed 's/ab/cd/'
   ```
   Output: `cdcde` (mengganti urutan konkatenasi dari regexp1 dan regexp2)

- `\n` (cocok dengan karakter baris baru):
  ```bash
  echo -e "line1\nline2" | sed '/line1\nline2/p'
  ```
  Output: `line1` diikuti oleh baris baru, kemudian `line2`

- `\char` (cocok dengan karakter khusus):
  ```bash
  echo "3.14" | sed 's/3\.14/pi/'
  ```
  Output: `pi` (mengganti "3.14" dengan "pi", di mana titik di-escape dengan backslash)

- `abcdef` (cocok dengan string eksak):
  ```bash
  echo "abcdef" | sed 's/abcdef/ABCDEF/'
  ```
  Output: `ABCDEF` (mengganti "abcdef" dengan "ABCDEF")

- `a*b` (nol atau lebih 'a' diikuti oleh 'b'):
  ```bash
  echo "aaab" | sed 's/a*b/x/'
  ```
  Output: `x` (mengganti nol atau lebih 'a' diikuti oleh 'b' dengan "x")

- `a\?b` (nol atau satu 'a' diikuti oleh 'b'):
  ```bash
  echo "ab" | sed 's/a\?b/x/'
  ```
  Output: `x` (mengganti nol atau satu 'a' diikuti oleh 'b' dengan "x")

- `a\+b\+` (satu atau lebih 'a' diikuti oleh satu atau lebih 'b'):
  ```bash
  echo "aaabbb" | sed 's/a\+b\+/x/'
  ```
  Output: `x` (mengganti satu atau lebih 'a' diikuti oleh satu atau lebih 'b' dengan "x")

- `.*` dan `.\+`:
   - `.*` cocok dengan semua karakter dalam string, termasuk string kosong:
     ```bash
     echo "" | sed 's/.*/match/'
     ```
     Output: `match`
   - `.\+` cocok hanya dengan string yang mengandung setidaknya satu karakter:
     ```bash
     echo "content" | sed 's/.*/match/'
     ```
     Output: `match`

- `^main.*(.*)` (string dimulai dengan 'main', diikuti oleh tanda kurung buka dan tutup):
   ```bash
   echo "main()" | sed '/^main.*(.*)/p'
   ```
   Output: `main()`

- `^#` (string dimulai dengan '#'):
   ```bash
   echo "#comment" | sed '/^#/p'
   ```
   Output: `#comment`

- `\\$` (string berakhir dengan backslash tunggal):
   ```bash
   echo "end\\" | sed '/\\$/p'
   ```
   Output: `end\`

- `\[^ tab]\+` (string dari satu atau lebih karakter, tidak ada yang merupakan spasi atau tab):
   ```bash
   echo "word1 word2" | sed '/[^ \t]\+/p'
   ```
   Output: Cocok dengan setiap kata yang tidak mengandung spasi atau tab
