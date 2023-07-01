# Regex

string regexPattern = @"^(?!.*\.{2})(?!.*[&=_'\-+,<>])(?!.*\.$)[a-zA-Z0-9][a-zA-Z0-9.]*[a-zA-Z0-9]$";

Penjelasan regex:

1. ^ menandakan awal dari string.
2. (?!.*\.{2}) adalah negative lookahead yang memastikan tidak ada lebih dari satu titik berturut-turut.
3. (?!.*[&=_'\-+,<>]) adalah negative lookahead yang memastikan tidak ada karakter yang tidak diizinkan seperti tanda ampersand (&), sama dengan (=), garis bawah (_), apostrof ('), tanda hubung (-), tanda tambah (+), koma (,), tanda kurung (<,>).
4. (?!.*\.$) adalah negative lookahead yang memastikan tidak ada titik sebagai karakter terakhir.
5. [a-zA-Z0-9] adalah karakter pertama yang harus berupa huruf atau angka.
6. [a-zA-Z0-9.]* adalah karakter-karakter selanjutnya yang dapat berupa huruf, angka, atau titik.
7. [a-zA-Z0-9]$ adalah karakter terakhir yang harus berupa huruf atau angka.
8. $ menandakan akhir dari string.

string regexPattern = "^\\w+([.]\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$"

Penjelasan regex : 
1. ^ : Menandakan awal dari string. Ini memastikan bahwa keseluruhan string harus cocok dengan pola yang didefinisikan.
2. \\w+ : Mencocokkan satu atau lebih karakter huruf, angka, atau garis bawah (underscore) sebagai bagian dari nama pengguna email.
3. ([.]\\w+)* : Grup pengecualian yang mencocokkan titik (dot) dan satu atau lebih karakter huruf atau angka setelahnya. Ini memungkinkan penggunaan titik dalam nama domain, seperti dalam subdomain atau nama file. Tanda asterisk (*) menunjukkan bahwa grup pengecualian dapat muncul nol kali atau lebih.
4. @ : Mencocokkan karakter at (@) yang digunakan sebagai pemisah antara nama pengguna dan domain email.
5. \\w+ : Mencocokkan satu atau lebih karakter huruf atau angka sebagai bagian dari nama domain.
6. ([-.]\\w+)* : Grup pengecualian yang mencocokkan tanda hubung atau garis bawah diikuti oleh satu atau lebih karakter huruf atau angka. Ini memungkinkan penggunaan tanda hubung atau garis bawah dalam nama domain. Grup pengecualian ini juga dapat muncul nol kali atau lebih.
7. \\. : Mencocokkan titik (dot) sebagai pemisah antara domain dan ekstensi domain.
8. \\w+ : Mencocokkan satu atau lebih karakter huruf atau angka sebagai bagian dari ekstensi domain.
9. ([-.]\\w+)* : Grup pengecualian yang mencocokkan tanda hubung atau garis bawah diikuti oleh satu atau lebih karakter huruf atau angka. 
10. $ : Menandakan akhir dari string. Ini memastikan bahwa keseluruhan string cocok dengan pola yang didefinisikan hingga akhir.

## Sample
<code>
 var emails = new List<string>(){
            // Email tidak valid
                "astrid..ajalah@gmail.com",
                "astri&astrid@gmail.com",
                "astrid=astrid@gmail.com",
                "astrid'astrid@gmail.com",
                "astrid-astrid@gmail.com",
                "astrid+astrid@gmail.com",
                "astrid,astrid@gmail.com",
                "astrid<astrid@gmail.com",
                "astrid>astrid@gmail.com",
                "astrid..astrid@gmail.com",
                ".astrid@gmail.com",
                "astrid@gmail.com.",
                "astrid!123@gmail.com",
                "astrid/astrid@gmail.com",
                "astrid/ngarisbaru@gmail.com",
                "astrid\backSlash@gmail.com",
            // Email valid
                "astrid.astrid@gmail.com",
                "astrid_astrid@gmail.com",
                "astrid_astrid123@gmail.com",
                "Astrid@gmail.COM"
            };
            
            string regexPattern = "^[a-zA-Z0-9._]+@[a-zA-Z0-9-]+(?:\\.[a-zA-Z0-9-]+)*$";
            Regex regex = new Regex(regexPattern);

            foreach(var email in emails)
            {
                if (!regex.IsMatch(email))
                {
                    Console.WriteLine($"Email tidak valid : {email}");
                }
            }
</code>
