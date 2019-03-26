# Minggu 03

# Pengenalan Docker

Di sini akan dijelaskan bagaimana mendeploy docker container pertama kali kemudian mendeploy static HTML sebagai container dan juga bagaimana membangun container image. Untuk kali ini akan menggunakan katacod, untuk itu sebelum memulainya harus mempunyai akun di [https://www.katacoda.com/](https://www.katacoda.com/) 

## Mendeploy Docker Coantianer Pertama Kali
Langkah - Langkah 

1. Setelah berhasil login selanjutnya masuk ke course docker [https://www.katacoda.com/courses/docker/](https://www.katacoda.com/courses/docker/)

2. Kemudian Pilih Deploying Your First Docker Container
   ![02](images/1.PNG)

3. Klik Start Scenario
   ![03](images/2.PNG)

4. Kemudian mengetikan perintah ```docker search redis```

   ![04](images/3.PNG)

   Perintah di atas digunakan untuk mencari sebuah docker image untuk redis

5. Selanjutnya menjalankan docker image di background dengan mengetikan perintah ```docker run -d redis```

   ![05](images/4.PNG)

6. Setelah menjalankan docker image, untuk melihat container apa saja yang berjalan maka ketikan perintah ```docker ps```

   ![06](images/5.PNG)

    terlihat pada gambar di atas informasi lengkap tentang cointainer yang berjalan

7. Langkah berikutnya adalah mengexpose container yang sudah berjalan  

   ![07](images/6.PNG)

    Maksud dari sintaks di atas adalah akan menjalankan container redis di background dengan nama redisHostPort

8. Setelah menggunakan port -p hostport : container port, kali ini akan mencoba mengetikan hanya hostport saja yang diketikan 

    ![08](images/7.PNG)

9. Untuk mengetahui port container nya dengan mengetikan perintah ```docker port redisDynamic 6379```

   ![09](images/8.PNG)

10. Untuk mengetahui cointainer yang berjalan ketikan perintah ```docker ps```

    ![010](images/9.PNG)

11. Selanjutnya akan menyimpan data di luar container yaitu di docker host

    ![011](images/10.PNG)

12. Selanjutnya menjalankan Ubuntu contianer sekaligus melihat prosesnya pada contianer.

    ![012](images/11.PNG)

13. Untuk dapat mengakses bash dari dalam container maka ketikan perintah ```docker run -it ubuntu bash```.
 
    ![013](images/12.PNG)

14. Maka course pertama untuk docer pada katacoda telah selesai
    ![014](images/congrats1.PNG)


## Mendeploy website dan menggunakan nginx

Langkah - Langkah 

1. Yang harus pertama kali dilakukan adalah membuat dockerfile. Dockerfile digunakan untuk membuat image 

    ![01](images/nginx_1.png)
    
    Baris pertama mendifiniskan image sedangkan baris ke dua mengcopy content ke lokasi dalam container, sedangkan untuk index.html sendiri isinya adalah ```<html> Hello World </html>``` 

2. Buat html tersbut menjadi image menggunakan build command
   ```docker build -t webserver-image:v1 .```
   
3. Periksa image dengan menggunakan ```docker images```

    ![03](images/nginx_2.png)

4. Launching image yang telah dibuat menggunakan nama dan tag yang mudah, dan dikarenakan sebagai webserver maka port yang digunakan adalah 80
   ```docker run -d -p 80:80 webserver-image:v1```

5. Akses dengan mengetikan perintah ```curl docker``` hasilnya
    
    ![05](images/nginx_3.png)

6. Akses juga bisa dilakukan melalui browser sesuai link yang sudah disediakan oleh katacoda maka hasilnya akan seperti di bawah ini
    
    ![06](images/nginx_4.png)

## Membuat Container Images

Langkah - Langkah 

1. Membuat dockerfile 
```bash
FROM nginx:1.11-alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

2. Selanjutnya membuat image dari dockerfile tersebut ```docker build -t my-nginx-image:latest```

    ![02](images/build_1.png)

3. Image diperiksa apakah sudah ditambahkan dengan image yang dibuat tadi 
    ![03](images/build_2.png)

4. Jalankan image agar bisa diakses dengan perintah ```docker run -d -p 80:80 my-nginx-image:latest1```

5. Akses web server dengan perintah ```curl -i http://docker```

    ![05](images/build_3.png)

6. Periksa container yang sedang berjalan dengna perintah ```docker ps```

    ![06](images/build_4.png)

Maka Pengenalan docker mulai dari pertama kali mendeploy cointainer sampai membuat image telah selesai.

## Dwi Astuti