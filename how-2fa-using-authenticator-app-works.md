2fa bisa dilakukan menggunakan authenticator app seperti google atau microsoft authenticator app. untuk bisa lebih memahami bagaimana cara kerjanya akan saya jelaskan melalui skenario berikut. 

sebagai contoh kita ingin mengaktifkan 2FA github. authenticator apps yang kita gunakan sebut saja authapp. 
- ketika kita ingin mengaktifkan 2FA, github akan generate QRCode yang mana QRCode ini adalah secret key 
- authapp akan scan dan simpan QRCode tersebut
- ketika kita login ke github, setelah input username dan password maka langkah berikutnya adalah github meminta untuk input 2FA code
- kita masuk ke authapp dan minta untuk generate 2FA code github 
- authapp menggunakan secret key untuk generate 2FA code (biasanya 6 digit)
- code ini hanya bisa digunakan dalam rentang waktu (time window) tertentu, biasanya 30 detik 
- kita input code ini ke github 
- github akan melakukan verifikasi

bagaimana github melakukan verifikasi? 
- authapp dan github menggunakan secret key yang sama
- authapp dan github menggunakan algorithma yang sama untuk menghasilkan 2FA code
- algoritma yang digunakan biasanya HMAC-SHA1
- time window merupakan salah satu parameter pada algoritma tsb
- 2FA code = HMAC-SHA1 (time window, secret key)
- jadi ketika 2FA yang dihasilkan oleh github dan authapp sama maka verifikasi berhasil dan user bisa masuk ke github
