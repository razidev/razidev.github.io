---
title: Membuat Basecode API dengan Node.JS PART 3
published: true
categories: code,Node.JS,Express,MongoDB
---
Hai dipembahasan sebelumnya saya telah membahas membuat [basecode API bagian 2](https://razidev.github.io/Membuat-Basecode-API-dengan-NodeJs-PT2) yang menjelaskan tentang pembuatan API create-user , pada pembahasan ini saya akan membuat API read(view user) dari user yang telah di register.

Sama seperti pembuatan API sebelumnya, kita harus membuat file **list-user.js** di folder **APIs**. Dan kerangka projectnya akan menjadi seperti ini: 

base-code-api
- APIs
    - list-user.js
    - register.js
    - route.js
- node-modules
- index.js
- package.json
- package-lock.json

didalam file **route.js**, kita tambahkan menjadi seperti ini: 

```js
const express = require('express'),
    router = express.Router();


let register = require('./register'),
    list = require('./list-user');

router.post("/register", register.Register);
router.get("/list-user", list.List);

module.exports = router;
```

dan didalam file **list-user.js**, kita ketikkan kodingan seperti ini: 

```js
const MongoClient = require('mongodb').MongoClient;

exports.List = (req, res, next) => {
    MongoClient.connect('mongodb://localhost:27017/belajar', (err, db) =>{
        if (err) throw err;
        db.db().collection('users').find({}).toArray(function(err, result) {
            if (err) throw err;
            res.status(200).json({
                status: 'ok',
                data: result
            });
        })
    });
    
}
```

lalu kita jalankan diterminal `npm start`, buka postman:

![list-user result](https://i.ibb.co/GttN020/capture-1.png)

ya seperti itu hasilnya kodingan view-user tidak begitu banyak logic. Kodingan diatas bisa kita parsing lagi agar tidak semua data ditampilkan. Dalam pembahasan selanjutnya saya akan membahas [API update data user](https://razidev.github.io/Membuat-Basecode-API-dengan-NodeJs-PT4).