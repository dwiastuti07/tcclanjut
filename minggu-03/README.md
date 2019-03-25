# Minggu 03

# Pengenalan Docker

## Mendeploy Docker Coantianer Pertama Kali

Untuk kali ini akan menggunakan katacod, untuk itu sebelum memulainya harus mempunyai akun di [https://www.katacoda.com/](https://www.katacoda.com/) 


Langkah - Langkah 

1. Setelah berhasil login selanjutnya masuk ke course docker [https://www.katacoda.com/courses/docker/](https://www.katacoda.com/courses/docker/)

2. Kemudian Pilih Deploying Your First Docker Container
![02](images/1.png)

3. Klik Start Scenario
![03](images/2.png)

4. Kemudian mengetikan perintah ```docker search redis```

![04](images/3.png)

Perintah di atas digunakan untuk mencari sebuah docker image untuk redis

5. Selanjutnya menjalankan docker image di background dengan mengetikan perintah ```docker run -d redis```

![05] (images/4.png)

6. Setelah menjalankan docker image, untuk melihat container apa saja yang berjalan maka ketikan perintah ```docker ps```

![06](images/5.png)

terlihat pada gambar di atas informasi lengkap tentang cointainer yang berjalan

7. Langkah berikutnya adalah mengexpose container yang sudah berjalan  

![07](images/6.png)

Maksud dari sintaks di atas adalah akan menjalankan container redis di background dengan nama redisHostPort

8. Setelah menggunakan port -p hostport : container port, kali ini akan mencoba mengetikan hanya hostport saja yang diketikan 

![08](images/7.png)

9. Untuk mengetahui port container nya dengan mengetikan perintah ```docker port redisDynamic 6379```

![09](images/8.png)

10. Untuk mengetahui cointainer yang berjalan ketikan perintah ```docker ps```

![010](images/9.png)

11. Selanjutnya akan menyimpan data di luar container yaitu di docker host

![011](images/10.png)

12. Selanjutnya menjalankan Ubuntu contianer sekaligus melihat prosesnya pada contianer.

![012](images/11.png)

13. Untuk dapat mengakses bash dari dalam container maka ketikan perintah ```docker run -it ubuntu bash``.
 
![013](images/12.png)

14. Maka course pertama untuk docer pada katacoda telah selesai
![014](images/congrats1.png)