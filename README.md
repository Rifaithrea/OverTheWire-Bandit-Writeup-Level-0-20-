# 🕵️ OverTheWire Bandit Writeup (Level 0–20)

> Wargame: https://overthewire.org/wargames/bandit/   

# Level 0 → 1

### Objective
Login ke server menggunakan SSH dan membaca file untuk mendapatkan password level berikutnya.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

```bash
ls
cat readme
```

### Concepts Learned
- SSH login
- Navigasi directory
- Membaca file dengan `cat`

---

# Level 1 → 2

### Challenge
Password berada pada file bernama `-`

```bash
cat ./-
```

### Concepts
- Handling special filename
- Relative path usage

---

# Level 2 → 3

### Challenge
Nama file mengandung spasi.

```bash
cat "spaces in this filename"
# atau
cat spaces\ in\ this\ filename
```

### Concepts
- Escaping karakter khusus
- Quoting string

---

# Level 3 → 4

```bash
cd inhere
ls -a
cat .hidden
```

### Concepts
- Hidden files
- `ls -a`

---

# Level 4 → 5

Menentukan file yang readable dari sekumpulan file.

```bash
file ./*
cat <file_yang_bertipe_ascii>
```

### Concepts
- Identifikasi tipe file dengan `file`

---

# Level 5 → 6

Kriteria:
- Human readable
- Size 1033 bytes
- Not executable

```bash
find . -type f -size 1033c ! -executable
cat <hasil>
```

### Concepts
- Filtering file dengan `find`
- Permission & size filtering

---

# Level 6 → 7

Kriteria:
- Owner: bandit7
- Group: bandit6
- Size: 33 bytes

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### Concepts
- Advanced file search
- Redirect error output

---

# Level 7 → 8

Password berada pada baris dengan kata tertentu.

```bash
grep millionth data.txt
```

### Concepts
- Text searching dengan `grep`

---

# Level 8 → 9

Password adalah satu-satunya baris unik.

```bash
sort data.txt | uniq -u
```

### Concepts
- Sorting & unique filtering

---

# Level 9 → 10

File binary dengan string tersembunyi.

```bash
strings data.txt | grep =
```

### Concepts
- Extract printable strings dari binary

---

# Level 10 → 11

Base64 encoded file.

```bash
base64 -d data.txt
```

### Concepts
- Encoding & decoding base64

---

# Level 11 → 12

ROT13 encoding.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### Concepts
- Substitution cipher
- Character translation

---

# Level 12 → 13

File dikompresi berlapis (gzip, bzip2, tar, dll).

Strategi:
1. Gunakan `file`
2. Rename sesuai tipe
3. Extract berulang

Contoh:

```bash
mv data.txt data.gz
gunzip data.gz
```

Ulangi hingga mendapat ASCII text.

### Concepts
- File type inspection
- Multi-layer compression handling

---

# Level 13 → 14

Login menggunakan SSH private key.

```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

### Concepts
- SSH key authentication

---

# Level 14 → 15

Password tersedia melalui koneksi TCP localhost port 30000.

```bash
echo "<password>" | nc localhost 30000
```

### Concepts
- Netcat
- Manual TCP communication

---

# Level 15 → 16

Menggunakan SSL connection.

```bash
openssl s_client -connect localhost:30001
```

### Concepts
- TLS handshake
- Secure socket connection

---

# Level 16 → 17

Scan port range 31000–32000 untuk menemukan service aktif.

```bash
nmap -p31000-32000 localhost
```

Kemudian gunakan SSL pada port yang benar.

### Concepts
- Port scanning
- Service discovery

---

# Level 17 → 18

Password adalah perbedaan antara dua file.

```bash
diff passwords.old passwords.new
```

### Concepts
- File comparison

---

# Level 18 → 19

Shell dibatasi, perlu bypass.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 -t bash
```

### Concepts
- Restricted shell bypass

---

# Level 19 → 20

Binary dengan SUID.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

### Concepts
- SUID
- Privilege escalation dasar

---

# Refleksi & Pembelajaran

Bandit 0–20 melatih:

- Linux CLI fundamental
- File permission & ownership
- Text processing
- Encoding & encryption dasar
- Compression handling
- Networking dasar (TCP & SSL)
- Automation & troubleshooting mindset

Bandit bukan tentang “hacking cepat”,  
tetapi tentang observasi detail, eksperimen, dan berpikir sistematis.

---

## 🧠 Next Step

Untuk melanjutkan penguatan skill:
- Selesaikan hingga Level 34
- Automasi beberapa challenge dengan scripting
- Dokumentasikan dengan analisis lebih mendalam (bukan hanya command)

---

📌 Repository ini dibuat sebagai dokumentasi pembelajaran dan referensi pribadi dalam memahami dasar sistem Linux dan security mindset.
