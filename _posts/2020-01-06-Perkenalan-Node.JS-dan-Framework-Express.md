---
title: Perkenalan Node.Js Dan Framework Express
published: true
categories: code
---
Hai fellows, adakah kalian yang baru ingin mempelajari node.js dan caranya membuat API(application programming interface). Jika iya, kalian berada di blog yang tepat. Pada artikel ini saya akan membahas apa itu node.js dan framework express. Let's get started...
![](https://cdn.pixabay.com/photo/2015/04/23/17/41/node-js-736399_960_720.png)

Node.js adalah platform berbasis javascript yang lebih digunakan untuk server-side atau bisa dieksekusi diluar browser dan bisa juga client-side karena Javascript sendiri merupakan bahasa pemrograman client-side atau pada browser. Dengan bantuan runtime pada javascript, kini memungkinkan developer membuat aplikasi berbasis web, mobile, ataupun membuat API yang berjalan diatas server. Node.js memiliki module http tersendiri yang memungkinkan developer membuat aplikasi berjalan di server web tanpa bantuan aplikasi lain seperti xampp, mamp, atau lainnya.

Yang membedakan node.js dengan bahasa pemrograman lain yaitu Nodej.s bersifat non-blocking/asynchronous yang merupakan mengeksekusi code tanpa harus menunggu code sebelumnya selesai terlebih dahulu. Karena non-blocking, sistem scalable sangat dianjurkan dikembangkan dengan Node.js. Berikut contoh code perbandingan dari blocking dan non-blocking.

```js
//Blocking Code
const fs = require('fs');
console.log('before reading');
console.log('reading file ', fs.readFileSync('/README.md'));
console.log('after reading'); // akan jalan setelah reading file
```

```js
//Non-BLocking Code
const fs = require('fs');
console.log('before reading');
fs.readFile('/README.md', (err, data) => {
	if (err) throw err;
	console.log('reading file', data);
});
console.log('after reading'); // akan jalan sebelum membaca file
```

Contoh pertama pada `blocking code` diatas, `console.log('reading file)` akan dipanggil terlebih dahulu sebelum `console.log('after reading')`. Sedangkan contoh kedua `non-blocking code`, fs.readFile() adalah non-blocking, jadi eksekusi bisa terus berlanjut dan `console.log('after reading')` akan dipanggil terlebih dahulu sebelum `console.log('reading file')`. Kelebihannya `console.log('after reading')` dipanggil terlebih dahulu tanpa harus menunggu file terbaca sampai selesai adalah kunci desain arsitektur untuk proses yang lebih cepat.

Framework express merupakan web application framework paling populer untuk Node.js yang digunakan untuk membuat web application ataupun REST API. Framework ini menjadi dasar framework server pada Node.js. Pada kategori Node.js ini saya hanya akan membahas membuat REST API dengan format JSON dan diharapkan pembaca sudah paham dasar-dasar dari pemrograman. Dimateri selanjutnya saya akan membahas Basecode API dari Node.js dan Express.js