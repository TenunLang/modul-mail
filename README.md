# modul-mail

Kirim email via SMTP untuk bahasa [Tenun](https://github.com/TenunLang/Tenun). Ditulis sepenuhnya dengan Tenun.

## Pasang

```
tenun add mail
```

## Pakai

```tenun
impor "mail";

biar r: bulat = mail_kirim(
    "127.0.0.1", 1025,        // server SMTP
    "", "",                   // pengguna, sandi (kosong = tanpa AUTH)
    "noreply@situs.id",       // pengirim
    "pengguna@contoh.id",     // tujuan
    "Selamat datang",         // subjek
    "Halo dari Tenun."        // isi
);
kalau r == 0 { cetak("terkirim"); }
```

Dengan autentikasi:

```tenun
mail_kirim("smtp.relay.id", 587, "user", "sandi", "dari@id", "ke@id", "Subjek", "Isi");
```

## Fungsi

- `mail_kirim(inang, port, pengguna, sandi, pengirim, tujuan, subjek, isi): bulat`
  Kirim satu email. Kembalikan `0` bila sukses, kode negatif bila gagal (mis. `-2` greeting, `-6` AUTH, `-8` RCPT). `pengguna`/`sandi` kosong = lewati `AUTH LOGIN`.

## Catatan TLS

Modul ini memakai SMTP **teks polos** (tanpa TLS). Cocok untuk:

- Relay/sink lokal saat pengembangan (MailHog, Mailpit, `localhost:25`).
- Server yang mengizinkan AUTH polos di jaringan tepercaya.

Untuk submission ber-TLS (port 465/587 wajib TLS), jalankan relay lokal sebagai perantara — TLS langsung belum didukung builtin Tenun. Header memakai CRLF dan dot-stuffing sesuai RFC 5321.

## Struktur

```
modul-mail/
  tenun.json
  src/mail.tenun
  contoh/contoh.tenun
```

## Lisensi

MIT.
