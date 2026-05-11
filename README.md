## Modul 9 - Software Architectures

### Reflection 1
1. What is amqp?
Advanced Message Queuing Protocol (AMQP) adalah protokol standar terbuka pada application layer yang dirancang khusus untuk middleware pengiriman pesan. AMQP bisa dianggap sebagai aturan bahasa standar agar berbagai sistem, layanan, atau aplikasi yang mungkin saja dikode ditulis dalam bahasa pemrograman yang berbeda bisa saling bertukar pesan secara aman dan efisien. AMQP mengatur bagaimana pesan dikirim, dimasukkan ke dalam queue, routing, dan diterima. Salah satu message broker yang menggunakan protokol AMQP adalah RabbitMQ.

2. What does it mean? `guest:guest@localhost:5672` , what is the first ***guest***, and what is the second ***guest***, and what is ***localhost:5672*** is for?
`guest:guest@localhost:5672` adalah suatu connection string (URL koneksi) yang digunakan oleh suatu client application untuk melakukan autentikasi dan terhubung ke server *message broker* AMQP seperti RabbitMQ. Format dari connection string tersebut adalah:
- ***guest*** yang pertama adalah username
- ***guest*** yang kedua adalah password
- ***localhost:5672*** adalah lokasi jaringan dari server broker. ***localhost*** adalah hostname dan ***5672*** adalah port default yang digunakan untuk traffic AMQP.