# Writeup CTF Responsi

### Reconnaisance
Scan subnet untuk host discovery menggunakan nmap

![Screenshot 2024-12-21 032612](https://github.com/user-attachments/assets/b04e455b-1123-472b-8cdf-bd3fc55b55db)

Scan open port atau running service menggunakan nmap

![image](https://github.com/user-attachments/assets/42966ba7-0523-454f-b5cd-98c49eab8da3)

### Initial Access
Terdapat open port 80 (http/web). akses web dan register ke web.

![image](https://github.com/user-attachments/assets/259746c4-d1f3-46bb-9b32-adda384b6ffa)

![image](https://github.com/user-attachments/assets/4b112efc-3fa2-4c88-8893-99e6435491de)

Setelah register, login sebagai user. setelah berhasil login user akan mendapatkan cookie dari server agar dapat diautentikasi.

![image](https://github.com/user-attachments/assets/ce40c8ee-a282-45fc-9f1e-2c93bdda5f3f)

Jika sudah terautentikasi sebagai user biasa di web. ganti cookie menjadi admin untuk memperoleh hak akses admin. cookie bisa dibuat dengan mengencode string "admin" ke base64. ganti cookie user dengan cookie admin. Klik logout atau reload halaman dan akan terautentikasi sebagai admin.

![image](https://github.com/user-attachments/assets/d3ca5114-1cc2-4080-9814-ecaaede02452)

admin memiliki hak akses lebih dari user biasa. admin bisa melakukan upload produk di halaman /product.php. di halaman product terdapat flag pertama.

![image](https://github.com/user-attachments/assets/86e67d78-c9ea-4bf6-b33c-f89c97baac72)

![Screenshot 2024-12-21 033119](https://github.com/user-attachments/assets/06cb0bd6-8cc8-4dba-9b15-de21e1f4f20f)


### Foothold
coba upload shell melalui fitur upload gambar produk. fitur upload akan membatasi upload gambar hanya dengan ekstensi tertentu.

![Screenshot 2024-12-21 034713](https://github.com/user-attachments/assets/3d6b69be-f01d-4253-8cff-6192efe50223)

jika halaman tersebut diinspect maka bisa melihat bahwa terdapat fiter untuk membatasi ekstensi file yang dapat di upload.

![image](https://github.com/user-attachments/assets/919df401-1a53-432f-a9e9-883d9ade2506)

namun karena filter berada di frontend bisa dilakukan bypass dengan cara intercept trafik menggunakan burpsuite dan modifikasi request sebelum dikirim ke server.

![Screenshot 2024-12-21 035610](https://github.com/user-attachments/assets/eab9f46b-3a04-439f-ba2b-d90789a41478)

buat php reverse shell, sesuaikan ip dan port dengan listener.

![image](https://github.com/user-attachments/assets/6cc32efd-89ac-48ea-b5a9-737873346d38)

set listener menggunakan nc.

![image](https://github.com/user-attachments/assets/5211c77d-5fba-48d0-abf8-e954328742f9)

ubah ekstensi php reverse shell ke png agar dapat diupload di web.
intercept trafik dengan burpsuite lalu upload php reverse shell yang sebelumnya sudah diubah ekstensinya.

![image](https://github.com/user-attachments/assets/db182696-f88b-4bfd-ac26-4cb234464ab9)

modifikasi request dengan mengubah kembali ekstensi php reverse shell dari .png ke .php lalu forward request tersebut.

![Screenshot 2024-12-21 035714](https://github.com/user-attachments/assets/da90c6d8-788a-494e-a69f-5b02e8cf82a8)

akses shell yang sudah diupload. shell akan terupload di direktori /assets/img

![image](https://github.com/user-attachments/assets/9f062bef-cf51-439b-a363-e81e0396b7e6)

![image](https://github.com/user-attachments/assets/d6d49ae8-db1e-44f5-a342-3c44ff747761)

cek nc listener, kita mendapat shell sebagai user www-data.

![image](https://github.com/user-attachments/assets/f9fb8e4b-19c0-4bb7-a4e7-22908839fe12)

### Privilege Escalation ke User
terdapat 2 cara untuk memperoleh privilege user :
- terdapat hint di direktori web (hint.txt : enumerate user & rockyou)
- terdapat file database di direktori web (backup.db)

untuk cara pertama bisa melakukan bruteforce ssh. pada tahap reconnaisance di awal diketaui bahwa terdapat port 22 (ssh) yang terbuka. berdasarkan hint yang diperoleh, kita dapat melakukan enumerasi user untuk mengetahui username dan kita bisa menggunakan wordlist rockyou sebagai password untuk melakukan bruteforce.

enumerasi user dengan mengecek file cat /etc/passwd. terdapat user tk22eh.

![image](https://github.com/user-attachments/assets/7ba5e784-a995-4326-8a78-e48594fd9bf8)

lakukan bruteforce ssh dengan hydra

![image](https://github.com/user-attachments/assets/8eb21e72-6b48-436c-8523-387c76ed8f11)

untuk cara kedua bisa menggunakan password admin yang ada di database. bisa diasumsikan bahwa user admin di web adalah user yang password-nya sama dengan user di server. enumerasi user di server dengan cara yang sama dengan cara pertama (cat /etc/passwd).

![image](https://github.com/user-attachments/assets/44327f3c-1451-4721-bf28-8236fa6b5f87)

login ke ssh dengan username (tk22eh) dan password ( - password di db - )

![image](https://github.com/user-attachments/assets/d7a6081a-3f0c-4dcb-bf04-ac785be7a27f)


### Privilege Escalation ke Root
terdapat cron job yang berjalan. cek cron job dengan perintah cat /etc/crontab.

![image](https://github.com/user-attachments/assets/a09d0c7d-2551-45e3-91d2-5b78d045fc55)

berdasarkan crontab bisa diketahui bahwa ada cron job yang berjalan. cron job menjalankan file .config/priv_esc.sh di direktori home user.

cek hak akses file tersebut dengan perintah ls -la. user tk22eh memiliki akses untuk memodifikasi file tersebut.

![image](https://github.com/user-attachments/assets/a517ddb3-41d5-4cb6-8575-ff69b6c42f47)

modifkasi isi file. ubah file tersebut menjadi reverse shell. isi file dengan payload reverse shell sehingga ketika cron job dieksekusi maka reverse shell akan tereksekusi.

![image](https://github.com/user-attachments/assets/5e8ac181-b0ee-4142-8066-4c35711f83b9)

setup listener dengan nc. tunggu hingga cron job tereksekusi dan boom berhasil mendapat shell sebagai root.

![image](https://github.com/user-attachments/assets/a506e24f-e9b7-4d29-9cd3-4171b21709b4)
