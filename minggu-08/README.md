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

## Deploy Container Using YAML Definitions
Salah satu yang paling umum pada object kubernets adalah deployment objectnya. Deployment object menjelaskan spesifikasi container yang diinginkan, berserta nama dan label yang digunakan dari bagian lain kubernets untuk saling terkoneksi. Semua object - object yang diinginkan dalam disimpan sebuah file `yaml`. 

1. Create Deployment
Buat sebuah file `yaml` dengan nama `deployment.yaml` :

```bash
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: webapp1
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: webapp1
    spec:
      containers:
      - name: webapp1
        image: katacoda/docker-http-server:latest
        ports:
        - containerPort: 80
```
Kemudian di-deploy dengan menggunakan perintah :

![1](images/yaml/1.png)

container webapp1 sudah di-deploy sesuai dengan yang diketikan pada file `deployment.yaml`. dan untuk memastikan deployment berjalan dapat menggunakan perintah `kubectl get deployment`

![2](images/yaml/2.png)

Sedangkan untuk melihat secara rinci dapat menggunakan perintah `kubetcl describe deployment webapp1`

![3](images/yaml/3.png)

2. Create Service
Kubernets mempunyai kapasitas networking yang powerful yang mengontrol bagaimana aplikasi saling berkomunikasi. Konfigurasi networking dapat juga dikontrol melalui YAML, untuk itu dibuat sebuah file `service.yaml` :

```bash
apiVersion: v1
kind: Service
metadata:
  name: webapp1-svc
  labels:
    app: webapp1
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30080
  selector:
    app: webapp1
```

Delpoy service dengan menggunakan perintah `kubectl create -f service.yaml`

![4](images/yaml/4.png)

Untuk melihat diskripsi tentang service dapat menggunakan perintah `kubetcl get svc`

![5](images/yaml/5.png)

Sedangkan untuk melihat informasi lebih detail dapat dilakukan seperti gambar di bawah ini :

![6](images/yaml/6.png)

Test dengan menggunakan perintah `curl`

![7](images/yaml/7.png)

3. Scale Deployment

Untuk menambahkan service maka dapat mengubah isi pada file `deployment.yaml` yaitu dengan mengubah jumlah replicas yang tadinya `replicas : 1` menjadi `replicas : 4` setelah mengubahnya deploy ulang dengan perintah `kubetcl apply -f deployment.yaml`

![8](images/yaml/8.png)

Periksa jumlah replika dengan perintah `kubetcl get deployment `

![9](images/yaml/9.png)

Periksa jumlah pods

![10](images/yaml/10.png)

Test menggunakan perintah `curl`

![11](images/yaml/11.png)


## Dwast







