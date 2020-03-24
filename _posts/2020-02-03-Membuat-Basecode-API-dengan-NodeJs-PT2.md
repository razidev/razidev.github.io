---
title: Membuat Basecode API dengan Node.JS PART 2
published: true
categories: code,Node.JS,Express,MongoDB
---
Hai dipembahasan sebelumnya saya telah membahas membuat [basecode API bagian 1](https://razidev.github.io/Membuat-Basecode-API-dengan-NodeJs), pada bagian ini saya akan melanjutkan pembahasan sebelumnya dengan menggunakan database Mongo, disini saya akan membuat(create) API register.

Pertama-tama kita masuk ke dalam folder base-code-api lalu didalamnya kita buat folder **APIs**(*penamaan bebas) lalu kita buat file **route.js** dan **register.js** didalam folder APIs. Kira-kira kerangka-nya menjadi seperti ini:

base-code-api
- APIs
    - route.js
    - register.js
- node-modules
- index.js
- package.json
- package-lock.json

Di dalam file index.js, kita tambahkan kodingannya menjadi seperti ini: 

```js
const express = require('express'),
  app = express(),
  bodyParser = require('body-parser'),
  PORT = 3000;

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended: true}));

const APIS = require('./APIs/route');

app.use("/", APIS);
app.use((req, res, next) => {
    const error = new Error("Not Found");
    error.status = 404;
    next(error);
});

app.listen(PORT, ()=> console.info(`Server has started on PORT: ${PORT}`))

module.exports = app;
```

dan didalam file **route.js** kita ketik kodingan menjadi seperti ini: 

```js
const express = require('express'),
    router = express.Router();


let register = require('./register');

router.post("/register", register.Register);

module.exports = router;
```

dan didalam file **register.js** kita ketik kodingannya menjadi seperti ini:

```js
const MongoClient = require('mongodb').MongoClient;

exports.Register = (req, res, next) => {
    console.log(req.body)
    MongoClient.connect('mongodb://localhost:27017/belajar', (err, db) =>{
        if (err) throw err;
        db.db().collection('users').insertOne(
            {
                full_name: req.body.full_name,
                email: req.body.email,
                password: req.body.password,
                telephone: req.body.telephone
            }
        ).then(succed => {
            // console.log('user berhasil dibuat', succed)
            res.status(200).json({
                status: 'ok',
                message: 'user berhasil dibuat'
            });

        }).catch(err => {
            // console.log('erUpdate', err)
            res.status(500).json({
                status: 'error',
                message: `user gagal dibuat ${err}`
            });
        })
    });
}
```
pertama-tama kita `npm install mongodb` terlebih dahulu. Kita tidak harus membuat database dan collectionsnya terlebih dahulu, karna kodingan diatas sudah secara otomatis terbuat database dan collectionsnya.

Pastikan dilaptop anda sudah menginstall [mongodb](https://www.mongodb.com/download-center/community) ya. Lalu kita jalankan dengan `npm start` dan buka postman.

![register result](https://i.ibb.co/18Hj7cc/register-result.png)

Method:     POST

Body:   {"email": "razidev@mail.com" "full_name": "Razidev Blog","password": "pasword123" "telephone": "08912345678"}

Result: {"status": "ok", "message": "user berhasil dibuat"}

jika lihat di mongodb hasilnya seperti ini:

![database result](https://i.ibb.co/2grGgSh/mongodb-result.png)

Kodingan diatas bisa di improve lagi, misalkan password kita bisa encryp lagi menggunakan modul `bcrypt`, lalu anda bisa menggunakan `validator` tiap object agar tidak ada pengecekan satu persatu, dan menggunakan modul `mongose`. Anda bisa searching lebih lanjut di [npmjs](npmjs.com).

Untuk pembahasan membuat user sampai disini saja, selanjutnya saya akan membuat API melihat user.