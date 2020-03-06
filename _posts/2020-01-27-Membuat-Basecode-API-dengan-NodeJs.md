---
title: Membuat Basecode API dengan Node.JS PART 1
published: true
categories: code,Node.JS,Express
---
Hai sebelum masuk ke pembahasan, siapa yang pernah mengalami kesulitan mencari tutorial best practice dalam pembuatan aplikasi menggunakan bahasa pemrograman apapun? Pasti seorang software engineer pernah mengalami kesulitan mencari best practice mengkoding dalam bahasa pemrograman apapun entah dalam berapa lama sampai seorang tersebut merasa yakin bahwa yang dia koding sekarang merupakan best practice, mudah di reuse, mudah di debuging, dan lain-lain.

Pada pembahasan kali ini saya ingin membahas **_membuat basecode API dengan Node.JS + framework Express_** yang menurut saya ini best practice untuk saya sendiri. Diharapkan pembaca sudah menginstall [Node.Js](https://nodejs.org/en/). Pertama-tama anda ketikkan di terminal `npm init -y` didalam folder yang anda buat misal: **base-code-api** lalu akan terbuat file **package.json** jika dibuka maka dalamnya seperti ini:

```js
{
  "name": "base-code-api",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

dibagian object **main** terlihat jelas bahwa default file yang terbuat adalah **index.js**, maka dari itu kita buat file **index.js** diroot utama project node.js kita atau tepat dalam folder **base-code-api**

lalu kita bisa edit dari **package.json** dibagian object **scripts** kita bisa nambah object start menjadi seperti ini:
```js
{
	//tetap-sama
	"scripts": {
		"start": "nodemon index.js",
		"test": "echo \"Error: no test specified\" && exit 1"
	}
	//tetap-sama
}
```

lalu kita ketik di terminal `npm install nodemon express` maka akan terbentuk folder **node_modules** dan file **package-lock.json**, kita diamkan saja folder dan file tersebut karna keduanya merupakan digenerate secara otomatis oleh npm kita. Kira-kira perubahan dalam file **package.json** menjadi seperti ini:

```js
{
  "name": "base-code-api",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "nodemon": "^2.0.2"
  }
}
```

Mengapa menggunakan `nodemon` ? karna dengan nodemon jika ada perubahan dalam file, maka kita tidak harus merestart server kita. Cara menjalankan hanya dengan ketikkan di terminal `npm start`. Dan mengapa menginstall modul `express` ? karna dengan framework express kita dengan mudah terbantu dalam pengembangan API dan juga sudah banyak digunakan.

Lanjut lagi, dibagian file **index.js**, kita ketikkan kodingan seperti ini: 

```js
const express = require('express'),
  app = express(),
  bodyParser = require('body-parser'),
  PORT = 3000;

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended: true}));

app.listen(PORT, ()=> console.info(`Server has started on PORT: ${PORT}`))

module.exports = app;
```

Jika kita jalankan dengan `npm start` kira-kira di terminal akan muncul seperti ini:

```sh
Server has started on PORT: 3000
```

kira-kira seperti itu bagian pertama kerangka dari pembuatan API, bagian kedua akan dibahas dalam waktu yang akan datang.