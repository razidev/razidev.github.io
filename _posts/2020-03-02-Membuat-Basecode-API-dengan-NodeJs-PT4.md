---
title: Membuat Basecode API dengan Node.JS PART 4
published: true
categories: code,Node.JS,Express,MongoDB
---
Hai dipembahasan sebelumnya saya telah membahas membuat [basecode API bagian 3](https://razidev.github.io/Membuat-Basecode-API-dengan-NodeJs-PT3) yang menjelaskan tentang pembuatan API list-user, pada pembahasan ini saya akan membuat API **update user** yang telah saya buat user-nya dibagian sebelumnya.

Sama seperti pembuatan API sebelumnya, kita harus membuat file **update-user.js** di folder **APIs**. Dan kerangka projectnya akan menjadi seperti ini:

base-code-api
- APIs
    - list-user.js
    - register.js
    - route.js
    - update-user.js
- node-modules
- index.js
- package.json
- package-lock.json

didalam file **route.js**, kita tambahkan menjadi seperti ini:

```js
const express = require('express'),
    router = express.Router();


let register = require('./register'),
    updateUser = require('./update-user'),
    list = require('./list-user');

router.post("/register", register.Register);
router.get("/list-user", list.List);
router.post("/update-user", updateUser.UpdateUser);

module.exports = router;
```

dan didalam file **update-user**, kita ketikkan kodingan seperti ini:

```js
const MongoClient = require('mongodb').MongoClient,
    ObjectId = require('mongodb').ObjectID,
    bcrypt = require("bcrypt");

exports.UpdateUser = (req, res, next) => {
    MongoClient.connect('mongodb://localhost:27017/belajar', (err, db) =>{
        if (err) throw err;
        db.db().collection('users').updateOne({_id: ObjectId(req.body._id)}, {$set: {
            full_name: req.body.full_name,
            password: bcrypt.hashSync(req.body.password, 8)
        }}).then(updated => {
            res.status(200).json({
                status: 'ok',
                message: 'sukses update user'
            });
        }).catch(err => {
            res.status(200).json({
                status: 'ok',
                message: `Gagal update ${err}`
            });
        })
    });
}
```

Diatas kodingan tersebut saya memakai module bcrypt untuk mengenkripsi password yang diinput agar kerahasiaan user lebih terjaga. Untuk user yang ingin saya edit adalah user dengan full name _Quality Asurance_

![list-user](https://i.ibb.co/wwbzyDp/Capture.png)

lalu kita jalankan diterminal `npm start`, buka postman dan hit api **update-user**:

![update-user result](https://i.ibb.co/MngM2zD/Capture.png)

dan kita cek API **list-user**:

![list-user](https://i.ibb.co/tJG7LMc/Capture.png)

Seperti itu kodingan dari **update-user** dengan logic yang simple. Dalam situasi tertentu untuk **update-user** banyak yang harus divalidasi datanya agar tidak ada kesalahan yang disengaja maupun tidak sengaja karna menyangkut data user yang sensitif. Dan dalam pembahasan selanjutnya saya akan membahas [delete user](https://razidev.github.io/Membuat-Basecode-API-dengan-NodeJs-PT5).