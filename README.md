## Modul 9 - Software Architectures

### Task 1
1. What is amqp?
Advanced Message Queuing Protocol (AMQP) adalah protokol standar terbuka pada application layer yang dirancang khusus untuk middleware pengiriman pesan. AMQP bisa dianggap sebagai aturan bahasa standar agar berbagai sistem, layanan, atau aplikasi yang mungkin saja dikode ditulis dalam bahasa pemrograman yang berbeda bisa saling bertukar pesan secara aman dan efisien. AMQP mengatur bagaimana pesan dikirim, dimasukkan ke dalam queue, routing, dan diterima. Salah satu message broker yang menggunakan protokol AMQP adalah RabbitMQ.

2. What does it mean? `guest:guest@localhost:5672` , what is the first ***guest***, and what is the second ***guest***, and what is ***localhost:5672*** is for?
`guest:guest@localhost:5672` adalah suatu connection string (URL koneksi) yang digunakan oleh suatu client application untuk melakukan autentikasi dan terhubung ke server *message broker* AMQP seperti RabbitMQ. Format dari connection string tersebut adalah:
- ***guest*** yang pertama adalah username
- ***guest*** yang kedua adalah password
- ***localhost:5672*** adalah lokasi jaringan dari server broker. ***localhost*** adalah hostname dan ***5672*** adalah port default yang digunakan untuk traffic AMQP.

### Task 2
1. How much data your publisher program will send to the message broker in one run?
Program publisher akan mengirimkan 5 buah pesan ke message broker dalam satu kali eksekusi. Hal ini terlihat dari 5 baris pemanggilan fungsi `p.publish_event()` secara berurutan di dalam fungsi `main()`. Masing-masing fungsi mengirimkan data `UserCreatedEventMessage` untuk pengguna Amir, Budi, Cica, Dira, dan Emir.

2. The url of: "amqp://guest:guest@localhost:5672" is the same as in the subscriber program, what does it mean?
Artinya program publisher dan subscriber terhubung ke server message broker yang sama yaitu `amqp://guest:guest@localhost:5672`.

### Task 3
Gambar RabbitMQ sudah bekerja
![RabbitMQ Running](static/rabbitmq_running.png)