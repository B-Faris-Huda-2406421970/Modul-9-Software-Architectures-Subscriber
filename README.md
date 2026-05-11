## Modul 9 - Software Architectures

### Task 1
---
1. What is amqp?
Advanced Message Queuing Protocol (AMQP) adalah protokol standar terbuka pada application layer yang dirancang khusus untuk middleware pengiriman pesan. AMQP bisa dianggap sebagai aturan bahasa standar agar berbagai sistem, layanan, atau aplikasi yang mungkin saja dikode ditulis dalam bahasa pemrograman yang berbeda bisa saling bertukar pesan secara aman dan efisien. AMQP mengatur bagaimana pesan dikirim, dimasukkan ke dalam queue, routing, dan diterima. Salah satu message broker yang menggunakan protokol AMQP adalah RabbitMQ.

2. What does it mean? `guest:guest@localhost:5672` , what is the first ***guest***, and what is the second ***guest***, and what is ***localhost:5672*** is for?
`guest:guest@localhost:5672` adalah suatu connection string (URL koneksi) yang digunakan oleh suatu client application untuk melakukan autentikasi dan terhubung ke server *message broker* AMQP seperti RabbitMQ. Format dari connection string tersebut adalah:
- ***guest*** yang pertama adalah username
- ***guest*** yang kedua adalah password
- ***localhost:5672*** adalah lokasi jaringan dari server broker. ***localhost*** adalah hostname dan ***5672*** adalah port default yang digunakan untuk traffic AMQP.

### Task 2
---
1. How much data your publisher program will send to the message broker in one run?
Program publisher akan mengirimkan 5 buah pesan ke message broker dalam satu kali eksekusi. Hal ini terlihat dari 5 baris pemanggilan fungsi `p.publish_event()` secara berurutan di dalam fungsi `main()`. Masing-masing fungsi mengirimkan data `UserCreatedEventMessage` untuk pengguna Amir, Budi, Cica, Dira, dan Emir.

2. The url of: "amqp://guest:guest@localhost:5672" is the same as in the subscriber program, what does it mean?
Artinya program publisher dan subscriber terhubung ke server message broker yang sama yaitu `amqp://guest:guest@localhost:5672`.

### Task 3
---
Gambar RabbitMQ sudah bekerja
![RabbitMQ Running](static/rabbitmq_running.png)

### Task 4
---
Gambar pengiriman dan pemrosesan event. Disini publisher akan mengirimkan 5 pesan ke RabbitMQ lalu subscriber menerima 5 pesan tersebut seperti yang terlihat pada terminal
![Sending and Receiving Event](static/sending_receiving_event.png)

### Task 5
---
Gambar spike pada grafik kedua. Disini spike terjadi karena subscriber menerima pesan dari queue dan selesai memprosesnya. Setiap kali subscriber memproses satu pesan, subscriber akan memberikan sinyal "Ack" berupa konfirmasi tanda terima ke RabbitMQ dan memperbolehkan RabbitMQ menghapusnya dari queue.
![Spike on Second Chart](static/spike.png)

### Task 6
---
Gambar grafik yang mensimulasikan slow response oleh subscriber. Berdasarkan gambar, dapat dilihat bahwa jumlah angka pada queue adalah 7 yang berarti ada 7 pesan pada queue. Jika kita melihat pada grafik kedua, kecepatan deliver yaitu manual ack (pengiriman pesan dari RabbitMQ ke subscriber) adalah 2 pesan per detik. Sedangkan, kecepatan konfirmasi dari subscriber yaitu consumer ack adalah 1 pesan per detik. Kesimpulannya, ada bottleneck di subscriber yang membuat konfirmasi pesan diterima menjadi lebih lambat dari kecepatan pesan dikirim oleh RabbitMQ. Ini sesuai dengan perubahan kode yang kita lakukan yaitu menambahkan `thread::sleep()` pada `main()` di subscriber. 
![Slow Response Graph](static/slow_response.png)

### Task 7
---
Gambar grafik yang menunjukkan penerimaan pesan menjadi lebih efisien karena tugas menerima pesan dibagi ke 4 subscriber.
Sebelumnya, pada grafik bagian bawah, consumer ack (garis ungu) kurang mampu mengimbangi manual ack (garis merah) karena adanya delay response pada subscriber. Sekarang, pada grafik bagian bawah dapat dilihat bahwa consumer ack dapat mengimbangi manual ack karena beban (load) dari pesan-pesan yang ada pada queue dibagi-bagikan ke 4 subscriber tersebut oleh RabbitMQ (load balancing). Akibatnya, agregat dari pesan konfirmasi oleh subscriber menjadi lebih cepat dan mampu mengimbangin kecepatan manual ack.
![Multi-subscriber Graph](static/multi_subs.png)


### Bonus
---
1. Gambar RabbitMQ sudah bekerja. Disini saya menggunakan hosting cloud dari [CloudAMPQ](https://www.cloudamqp.com/) untuk hosting RabbitMQ-nya.
![RabbitMQ Running on Cloud](static/cloud_rabbitmq.png)

2. Gambar penerimaan pesan oleh subscriber. Dapat dilihat dari sini bahwa pesan dari publisher berhasil dikirim ke RabbitMQ yang dijalankan di cloud. RabbitMQ kemudian mengirim pesan ke listener-nya yaitu program subscriber. Pesan diterima oleh subscriber dan diproses seperti yang terlihat pada terminal.
![Receiving Messages from Cloud](static/cloud_receiving.png)

3. Gambar chart yang menujukkan bahwa publisher mengirim pesan dan subscriber menerimanya dari dashboard RabbitMQ yang dijalankan di cloud. Ini bisa dilihat dari spike yang berada di ujung kiri chart kedua.
![Monitong RabbitMQ on Cloud](static/cloud_monitoring.png)

4. Gambar chart yang mensimulasikan slow subscriber. Disini publisher mengirimkan banyak pesan, tetapi hanya ada satu subscriber yang siap menerima pesan tersebut. Akibatnya, consumer ack kurang mampu mengimbangi manual ack seperti yang dilihat pada chart bagian bawah.
![Slow Response Graph on Cloud](static/cloud_slowresponse.png)