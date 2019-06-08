# minggu-08
# Kubernet

Kubernetes adalah platform open-source berbasis Linux yang dirancang untuk mengotomatisasi penempatan, penskalaan, dan manajemen aplikasi yang berada dalam kontainer. Dengan Kubernetes, Anda dapat dengan cepat dan efisien menanggapi permintaan pelanggan.
Untuk mendeploy container akan digunakan dua cara yaitu menggunakan kubectl dan YAML.

## Kubetcl
1. Untuk memulainya perlu me-launch sebuah kubernet cluster dengan mengetikan command `minikube start`

![1](images/1.png)

Kemudian periksa nodes yang siap digunakan dengan mengetikan perintah `kubetcl get nodes`

![2](images/2.png)

Terlihat dari gambar di atas bahwa minikube siap untuk digunakan dan versinya adalah v1.13.3

2. Setelah itu jalankan kubectl, untuk menjalankannya menggunakan perintah `kubetcl run <name of deployment><properties>`

![3](images/3.png)

images yang dijalankan adalah diambil dari `katacoda/docker-http-server:latest`

untuk melihat status dari deployment dapat menggunakan perintah `kubetcl get deployments`

![4](images/4.png)

Dari gambar di atas terlihat bahwa http siap untuk digunakan.

Untuk melihat proses deployment secara rinci dapat menggunakan perintah `kubetcl describe deployment http`

![5](images/5.png)

3. Kubectl Expose
Untuk mengekspose service ke sebuah port sehingga dapat diakses dapat menggunakan perintah `kubetcl expose`

![6](images/6.png)

Maksud dari perintah di atas adalah akan mengekspose container pada mesin menggunakan port 80 sedangan untuk external-ip menggunakan port 8080, Sehingga apabila akan mengkases perlu menambahkan 8080 setelah ip 172.17.0.15.
Untuk memeriksanya dapat dilakukan dengan cara ping ke mesin dengan mengetikan perintah `curl http://172.17.0.15:8080`

![7](images/7.png)

4. Jalankan dan Expose Kubetcl
Untuk membuat service http kedua pada port 8001 dapat menggunakan perintah di bawah ini

![8](images/8.png)

Untuk melihat apakah service kedua berhasil dapat menggunakan perintah `curl`

![9](images/9.png)

Dengan peritah `kubetcl get svc` maka service tidak dapat muncul .

![10](images/10.png)

Untuk melihat detailnya dapat menggunakan perintah `docker ps | grep httpexposed`

![11](images/11.png)

5. Scale Containers
Setelah Service berjalan, kita dapat mengatur berapa pods yang akan dijalankan.

![12](images/12.png)

Dengan demikian pods yang akan dijalankan adalah 4, dapat dilihat dengan perintah `kubetcl get pods`

![13](images/13.png)

Masing - masing pod akan ditambahkan ke dalam load balancer, dengan perintah `kubetcl describe svc http` akan ditampilkan diskripsi lengkap tentang pods 

![14](images/14.png)

Kemudian test mengunggankan perintah `curl`

![15](images/15.png)

