# basic-knowledge

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
