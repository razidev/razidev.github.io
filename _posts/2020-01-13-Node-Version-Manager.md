---
title: Node Version Manager
published: true
categories: code,Node.JS
---
NVM merupakan kependekan dari Node Version Manager, dari namanya sudah jelas bahwa NVM bertugas sebagai memanage versi dari Node.JS kita, misalkan project yang teman anda kerjakan versi Node.Jsnya berbeda dengan versi Node.JS komputer kita dengan persyaratan Node.JS versi lama/baru tersebut mengharuskan komputer kita untuk menyesuaikan versinya agar tidak terjadi error. Maka dari pada anda uninstall/install Node.JS berulang kali, NVM membantu anda dalam hal ini dengan menginstall beberapa versi Node.JS dan menggunakan versi yang dibutuhkan.

Pertama-tama jalankan command dibawah ini
```sh
#linux

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
#atau
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
							#sumber: https://github.com/nvm-sh/nvm
```
copy 3 line terbawah hasil dari install command diatas, dan paste di terminal itu juga dan tekan enter.
```sh
#example
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
Tutup terminal anda dan buka kembali terminal baru. Cek `nvm --version` untuk mengecek versinya jika berhasil diinstall. Ketik `nvm ls` untuk melihat semua daftar versi Node.Js yang terinstall di komputer. Ketik `nvm  install ${version}` untuk menginstall versi Node.JS yang diinginkan. Dan `nvm use ${version}` untuk menggunakan versi Node.JS yang diinginkan

Saya kira cukup penggunaan yang sering digunakan di NVM dan anda bisa cek command `nvm --help` untuk penggunaan lebih lanjut

untuk pengguna windows installnya bisa baca [disini](https://github.com/coreybutler/nvm-windows)