# Minggu 06

# Docker Swarm

Docker swarm digunakan untuk membantu manajemen docker pada multiple host, dengan menggunakan docker swarm dapat membuat clustering dan juga penjadwalnya. Untuk melihat command - command yang dapat menggunakan perintah di bawah ini 

![01](images/swarm_1.png)

Langkah - Langkah 

## 1.  Initialise Swarm Mode 
    
  ![02](images/swarm_2.png)

   Command ```docker swar init``` digunakan untuk menginisialisasi docker host menjadi multiple docker host dengan demikian docker engine dapat digunakan untuk clustering dan berlaku sebagai manager. Selain itu command ini akan menghasilkan token yang digunakan untuk menambahkan node ke cluster.

## 2.  Join Cluster
    
   Cara mendapatkan token adalah mananyakan ke manager yang sudah berjalan via ``` swarm join-token`` dengan mengetikan command 

   ![03](images/swarm_3.png)

  setelah mendapatkan token dan disimpan pada variabel $token kemudian dapat digunakan untuk mendaftarkan host yang baru sebagai worker. Manager akan menerima node baru yang ditambahkan ke dalam cluster

   ![04](images/swarm_4.png)

   Kemudian diperiksa apakah node bertambah atau tidak dengan mengetikan command ```docker node ls```

   ![05](images/swarm_5.png)

## 3.  Create Overlay Network
    
   Overlay network dibuat agar container - container pada host yang lain dapat saling berkomunikasi. Virutal Extensible Lan (VXLAN) dirancang untuk cloud skala besar.

   ![06](images/swarm_6.png)

   Command di atas akan membuat overlay network baru dengan nama skynet. Semua containers yang terhubung ke network ini dapat saling berkomunikasi.

## 4.  Deploy Service
    
   ![07](images/swarm_7.png)

   Pada contoh ini docker image dibuat network skynet baru dengan nama katacoda/docker-http-server. Didefinisikan nama service adalah http kemudian di replica menjadi dua service setelah itu dilakukan load balance untuk service tersebut yang berjalan di port 80. Dengan demikian node yang menerima request bukan node yang menerima, akan tetapi docker load balances melakukan request ke semua container yang tersedia di dalam cluster.
   Untuk memeriksa apakah service dapat menggunakan command ``docker service ls``

   ![08](images/swarm_8.png)

   Selanjutnya periksa contianer pada host1 atau pada host manager
   
   ![09](images/swarm_9.png)

   Periksa juga container pada worker

   ![10](images/swarm_10.png)

   Kemudian periksa docker service dengan ```curl```

   ![11](images/swarm_11.png)

   Untuk memeriksa Container ID digunakan command ```docker service http```

   ![12](images/swarm_12.png)

## 5. Inspect State

    Kita dapat juga melihat detail dan konfigurasi servic

   ![13](images/swarm_13.png)

   Setiap node dapat diperiksa node mana yang sedang berjalan

   ![14](images/swarm_14.png)

   Dari command tersebut dapat didapatkan informasi status nodevsaat ini dan status node yang seharusnya (desired state). Jika status saat itu tidak sesuai yang diharapkan, field error akan terisi jenis errornya.

   Selanjutnya menambahkan ID node pada command di atas

   ![15](images/swarm_15.png)

   Untuk melihat service mana yang merespon request dapat menggunakan perintah ```curl```.

   ![16](images/swarm_16.png)

   Pada gambar di atas terlihat bahwa serice id yang merespon berbeda dengan sebelumnya dikarenakan dengan sistem load balancing, service akan mengirimkan request ke semua container yang berjalan pada cluster.

## 6. Scale Service
   
   Scale service adalah sebuah service pada docker yang mengizinkan melakukan scale up dari task yang berjalan pada cluster

   ![17](images/swarm_17.png)

   Command di atas akan membuat http service berjalan sebanyak 5 containers. Sedangkan untuk melihat masing - masing host dapat menggunakan command ```docker ps```
   
   ![18](images/swarm_18.png)

   Pada gambar di atas terlihat untuk setiap host terlihat ada penambahan node.

   Untuk melihat hasilnya dapat menggunakan perintah ```curl```
   
   ![19](images/swarm_19.png)


### by dwast


