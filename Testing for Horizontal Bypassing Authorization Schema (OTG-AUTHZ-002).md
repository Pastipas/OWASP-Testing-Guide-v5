Pengujian yang Melewati Skema Pengesahan Horizontal (OTG-AUTHZ-002)

Ringkasan
--------
Pengujian seperti ini berfokus pada memverifikasi bagaimana skema pengesahan Horizontal telah dijalankan untuk masing-masing peran atau keistimewaannya untuk mendapatkan hak mengakses data dan sumber-sumber dari pengguna-pengguna yang lain yang memiliki peran dan keistimewaan yang sama.
Melewati pengesahan Horizontal bisa terjadi ketika seorang penyerang mendapat akses ke lebih banyak sumber atau data dari yang biasanya diizinkan untuk mereka. Tingkat izin atau perubahan seperti tersebut mestinya akan dicegah oleh aplikasi. 
Untuk setiap fungsi, perand dan permintaan tertentu yang dijalankan oleh aplikasi selama tahap setelah-pengesahan, hal tersebut perlu untuk diverifikasi kemballi:
-	Apakah mungin untuk mengakses sumber-sumber yang seharusnya bisa diakses oleh pengguna yang memiliki identitas yang berbeda namun memiliki peran dan keistimewaan yang sama? 
-	Apakah memungkinkan untuk menjalankan fungsi-fungsi pada sumber-sumber tersebut yang seharusnya bisa diakses oleh pengguna yang memiliki identitas yang berbeda? 

Bagaimana melakukan Pengujian
------------
Untuk setiap peran:
1.	Daftar/buat dua pengguna dengan peran yang sama.
2.	BUat dan simpan dua sesi token yang berbeda untuk pengesahan aplikasi (satu sesi token untuk setiap pengguna).
3.	Untuk setiap permintaan, ganti parameter dan sesi token yang sesuai dari token satu ke token yang kedua dan periksa respon tiap-tiap token.
4.	Sebuah aplikai akan dianggap rentan jika responnya sama, berisi data rahasia yang sama atau mengindikasikan pengoperasian yang berhasil pada sumber-sumber atau data pengguna yang lain.

Sebagai contoh, anggap saja fungsi 'viewCCpincode.jsp' merupakan bagian dari setiap menu akun dari aplikasi dengan peran yang sama, dan memungkinkan untuk mengaksesnya dengan meminta URL berikut:
https://www.example.com/account/viewCCpincode.jsp 

Kemudian, permintaa HTTP berikut dibuat saat memanggil fungsi viewCCpincode:
POST /account/viewCCpincode.jsp HTTP/1.1
Host: www.example.com
[hulu HTTP yang lain]
Kuki: SessionID=xh6Tm2DfgRp01AZ03

Idpincode=pengguna1

Respon yang sahih dan tepat:
HTTP1.1 200 OK
[hulu HTTP yang lain]

{“pincode”:8432}
Penyerang akan mencoba menjalankan permintaan tersebut dengan parameter Idpincode yang saman:
POST /account/viewCCpincode.jsp HTTP/1.1
Host: www.example.com
[hulu HTTP yang lain]
Kuki: SessionID=GbcvA1_ATTACKER_SESSION_6fhTscd

Idpincode=pengguna1
Jika respon dari permintaan penyerang berisi data yang sama (“pincode”:8432) aplikasi dalam keadaan renta.

Peralatan
-------
Ekstensi Burp: Disahkan.
Rujukan
Standar Verifikasi Keamanan Aplikasi OWASP 3.0.1, V4.1, 4.4, 4.9, 4.16.
