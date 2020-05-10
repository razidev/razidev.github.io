---
title: Membuat Basecode API dengan Node.JS PART 5
published: true
categories: code,Node.JS,Express,MongoDB
---
Hai dipembahasan sebelumnya saya telah membahas membuat [basecode API bagian 4](https://razidev.github.io/Membuat-Basecode-API-dengan-NodeJs-PT4) yang menjelaskan tentang pembuatan API **update-user**, pada pembahasan ini saya akan membuat API **delete user** yang telah saya buat user-nya dibagian sebelumnya.

Sama seperti pembuatan API sebelumnya, kita harus membuat file **delete-user.js** di folder **APIs**. Dan kerangka projectnya akan menjadi seperti ini:

base-code-api
- APIs
    - delete-user.js
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
    list = require('./list-user'),
    deleteUser = require('./delete-user');

router.post("/register", register.Register);
router.get("/list-user", list.List);
router.post("/update-user", updateUser.UpdateUser);
router.delete("/delete-user/:user_id", deleteUser.DeleteUser);

module.exports = router;
```

dan didalam file **delete-user**, kita ketikkan kodingan seperti ini:

```js
const MongoClient = require('mongodb').MongoClient,
    ObjectId = require('mongodb').ObjectID;

exports.DeleteUser = (req, res, next) => {
    MongoClient.connect('mongodb://localhost:27017/belajar', (err, db) =>{
        if (err) throw err;
        db.db().collection('users').deleteOne({_id: ObjectId(req.params.user_id)})
        .then(deleted => {
            if (deleted.deletedCount) {
                res.status(200).json({
                    status: 'ok',
                    message: 'sukses delete user'
                });
            } else {
                res.status(200).json({
                    status: 'ok',
                    message: 'user tidak ditemukan'
                });
            }
        }).catch(err => {
            res.status(500).json({
                status: 'ok',
                message: `gagal delete user ${err}`
            });
        })
    });
}
```

Dalam kodingan pada file **delete-user** tidak ada module tambahan. Hanya berbeda dari querynya saja dengan menggunakan **deleteOne**, dan pemanggilan _user id_ tersebut saya menggunakan re.params, karna dalam **route.js** saya menangkap _user id_ dengan mengunakan parameter url dan saya menggunakan kondisi balikan dari **_deleted.deletedCount_**, jika dari console maka balikan dari **_deleted.deletedCount_** adalah 1(true) jika user terdelete atau 0(false) jika user tidak ada yang terdelete. Pertama-pertama user yang ingin saya delete adalah user dengan full name _Razidev Blog_ dengan id _5e81fe41511b3b18c8933e64_.

![list-user](https://i.ibb.co/TrZsGpj/delete-user1.png)

lalu kita jalankan diterminal `npm start`, buka postman dan hit api **delete-user**:

![delete-user result](https://i.ibb.co/r4FPt3B/api-delete.png)

dan kita cek API **list-user** dan **database**:

![api dan database](https://i.ibb.co/tYGvvn6/after-delete.png)

Dari hasil diatas kita bisa lihat bahwa di API **list-user** dan **database** usernya berkurang 1 dengan full name _Razi BLog_. Untuk materi membuat basecode API dengan NodeJS sampai disini, yang saya rasa cukup untuk pembahasan mengenai **CRUD**. Untuk projectnya ada bisa download atau clone di [Basecode API NodeJS](https://github.com/razidev/Basecode-API-NodeJS)