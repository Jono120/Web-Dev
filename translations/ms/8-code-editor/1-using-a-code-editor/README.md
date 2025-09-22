<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1ba61d96a11309a2a6ea507496dcf7e5",
  "translation_date": "2025-08-29T09:34:23+00:00",
  "source_file": "8-code-editor/1-using-a-code-editor/README.md",
  "language_code": "ms"
}
-->
# Menggunakan editor kod

Pelajaran ini merangkumi asas penggunaan [VSCode.dev](https://vscode.dev), sebuah editor kod berasaskan web, supaya anda boleh membuat perubahan pada kod anda dan menyumbang kepada projek tanpa perlu memasang apa-apa pada komputer anda.

## Objektif pembelajaran

Dalam pelajaran ini, anda akan belajar bagaimana untuk:

- Menggunakan editor kod dalam projek kod
- Menjejaki perubahan dengan kawalan versi
- Menyesuaikan editor untuk pembangunan

### Prasyarat

Sebelum anda bermula, anda perlu membuat akaun dengan [GitHub](https://github.com). Pergi ke [GitHub](https://github.com/) dan buat akaun jika anda belum memilikinya.

### Pengenalan

Editor kod adalah alat penting untuk menulis program dan bekerjasama dalam projek kod sedia ada. Setelah anda memahami asas editor dan cara menggunakan ciri-cirinya, anda boleh menerapkannya semasa menulis kod.

## Bermula dengan VSCode.dev

[VSCode.dev](https://vscode.dev) adalah editor kod di web. Anda tidak perlu memasang apa-apa untuk menggunakannya, sama seperti membuka laman web lain. Untuk bermula dengan editor ini, buka pautan berikut: [https://vscode.dev](https://vscode.dev). Jika anda belum log masuk ke [GitHub](https://github.com/), ikuti arahan untuk log masuk atau buat akaun baru dan kemudian log masuk.

Setelah dimuatkan, ia sepatutnya kelihatan seperti gambar ini:

![Default VSCode.dev](../../../../translated_images/default-vscode-dev.5d06881d65c1b3234ce50cd9ed3b0028e6031ad5f5b441bcbed96bfa6311f6d0.ms.png)

Terdapat tiga bahagian utama, bermula dari kiri ke kanan:

1. _Activity bar_ yang mengandungi beberapa ikon, seperti kaca pembesar 🔎, gear ⚙️, dan beberapa lagi.
2. _Side bar_ yang merupakan bar aktiviti yang diperluas, secara lalai dipanggil _Explorer_.
3. Dan akhirnya, kawasan kod di sebelah kanan.

Klik pada setiap ikon untuk memaparkan menu yang berbeza. Setelah selesai, klik pada _Explorer_ supaya anda kembali ke tempat asal.

Apabila anda mula mencipta kod atau mengubah kod sedia ada, ia akan berlaku di kawasan terbesar di sebelah kanan. Anda juga akan menggunakan kawasan ini untuk melihat kod sedia ada, yang akan anda lakukan seterusnya.

## Membuka repositori GitHub

Perkara pertama yang anda perlukan ialah membuka repositori GitHub. Terdapat beberapa cara untuk membuka repositori. Dalam bahagian ini, anda akan melihat dua cara berbeza untuk membuka repositori supaya anda boleh mula membuat perubahan.

### 1. Dengan editor

Gunakan editor itu sendiri untuk membuka repositori jauh. Jika anda pergi ke [VSCode.dev](https://vscode.dev), anda akan melihat butang _"Open Remote Repository"_:

![Open remote repository](../../../../translated_images/open-remote-repository.bd9c2598b8949e7fc283cdfc8f4050c6205a7c7c6d3f78c4b135115d037d6fa2.ms.png)

Anda juga boleh menggunakan _command palette_. _Command palette_ adalah kotak input di mana anda boleh menaip sebarang perkataan yang merupakan sebahagian daripada arahan atau tindakan untuk mencari arahan yang betul untuk dilaksanakan. Gunakan menu di bahagian atas kiri, kemudian pilih _View_, dan kemudian pilih _Command Palette_, atau gunakan pintasan papan kekunci berikut: Ctrl-Shift-P (pada MacOS ia adalah Command-Shift-P).

![Palette Menu](../../../../translated_images/palette-menu.4946174e07f426226afcdad707d19b8d5150e41591c751c45b5dee213affef91.ms.png)

Setelah menu dibuka, taip _open remote repository_, dan kemudian pilih pilihan pertama. Beberapa repositori yang anda sertai atau yang telah anda buka baru-baru ini akan muncul. Anda juga boleh menggunakan URL GitHub penuh untuk memilih satu. Gunakan URL berikut dan tampal ke dalam kotak:

```
https://github.com/microsoft/Web-Dev-For-Beginners
```

✅ Jika berjaya, anda akan melihat semua fail untuk repositori ini dimuatkan dalam editor teks.

### 2. Menggunakan URL

Anda juga boleh menggunakan URL secara langsung untuk memuatkan repositori. Sebagai contoh, URL penuh untuk repositori semasa ialah [https://github.com/microsoft/Web-Dev-For-Beginners](https://github.com/microsoft/Web-Dev-For-Beginners), tetapi anda boleh menukar domain GitHub dengan `VSCode.dev/github` dan memuatkan repositori secara langsung. URL yang terhasil ialah [https://vscode.dev/github/microsoft/Web-Dev-For-Beginners](https://vscode.dev/github/microsoft/Web-Dev-For-Beginners).

## Mengedit fail

Setelah anda membuka repositori pada pelayar/vscode.dev, langkah seterusnya ialah membuat kemas kini atau perubahan pada projek.

### 1. Cipta fail baru

Anda boleh mencipta fail di dalam folder sedia ada, atau menciptanya di direktori/folder akar. Untuk mencipta fail baru, buka lokasi/direktori di mana anda mahu fail disimpan dan pilih ikon _'New file ...'_ pada _activity bar_ _(kiri)_, beri nama dan tekan enter.

![Create a new file](../../../../translated_images/create-new-file.2814e609c2af9aeb6c6fd53156c503ac91c3d538f9cac63073b2dd4a7631f183.ms.png)

### 2. Edit dan simpan fail pada repositori

Menggunakan vscode.dev sangat berguna apabila anda ingin membuat kemas kini cepat pada projek anda tanpa perlu memuatkan sebarang perisian secara tempatan.  
Untuk mengemas kini kod anda, klik ikon 'Explorer', yang juga terletak pada _activity bar_ untuk melihat fail & folder dalam repositori.  
Pilih fail untuk membukanya di kawasan kod, buat perubahan anda dan simpan.

![Edit a file](../../../../translated_images/edit-a-file.52c0ee665ef19f08119d62d63f395dfefddc0a4deb9268d73bfe791f52c5807a.ms.png)

Setelah anda selesai mengemas kini projek anda, pilih ikon _`source control`_ yang mengandungi semua perubahan baru yang telah anda buat pada repositori anda.

Untuk melihat perubahan yang anda buat pada projek, pilih fail dalam folder `Changes` di _activity bar_ yang diperluas. Ini akan membuka 'Working Tree' untuk anda melihat secara visual perubahan yang anda buat pada fail. Warna merah menunjukkan penghapusan pada projek, manakala warna hijau menunjukkan penambahan.

![View changes](../../../../translated_images/working-tree.c58eec08e6335c79cc708c0c220c0b7fea61514bd3c7fb7471905a864aceac7c.ms.png)

Jika anda berpuas hati dengan perubahan yang anda buat, letakkan kursor pada folder `Changes` dan klik butang `+` untuk _stage_ perubahan tersebut. _Staging_ bermaksud menyediakan perubahan anda untuk dikomitkan ke GitHub.

Jika anda tidak selesa dengan beberapa perubahan dan ingin membatalkannya, letakkan kursor pada folder `Changes` dan pilih ikon `undo`.

Kemudian, taipkan `commit message` _(Deskripsi perubahan yang anda buat pada projek)_, klik ikon `check` untuk _commit_ dan _push_ perubahan anda.

Setelah selesai bekerja pada projek anda, pilih ikon `hamburger menu` di bahagian atas kiri untuk kembali ke repositori di github.com.

![Stage & commit changes](../../../../8-code-editor/images/edit-vscode.dev.gif)

## Menggunakan sambungan (extensions)

Memasang sambungan pada VSCode membolehkan anda menambah ciri baru dan pilihan persekitaran pembangunan yang disesuaikan pada editor anda untuk meningkatkan aliran kerja pembangunan anda. Sambungan ini juga membantu anda menambah sokongan untuk pelbagai bahasa pengaturcaraan dan sering kali sama ada sambungan generik atau sambungan berasaskan bahasa.

Untuk menyemak senarai semua sambungan yang tersedia, klik ikon _`Extensions`_ pada _activity bar_ dan mula menaip nama sambungan pada medan teks yang dilabelkan _'Search Extensions in Marketplace'_.  
Anda akan melihat senarai sambungan, setiap satu mengandungi **nama sambungan, nama penerbit, deskripsi satu ayat, jumlah muat turun** dan **penilaian bintang**.

![Extension details](../../../../translated_images/extension-details.9f8f1fd4e9eb2de5069ae413119eb8ee43172776383ebe2f7cf640e11df2e106.ms.png)

Anda juga boleh melihat semua sambungan yang telah dipasang sebelum ini dengan mengembangkan folder _`Installed`_, sambungan popular yang digunakan oleh kebanyakan pembangun dalam folder _`Popular`_, dan sambungan yang disyorkan untuk anda sama ada oleh pengguna dalam ruang kerja yang sama atau berdasarkan fail yang baru dibuka dalam folder _`Recommended`_.

![View extensions](../../../../translated_images/extensions.eca0e0c7f59a10b5c88be7fe24b3e32cca6b6058b35a49026c3a9d80b1813b7c.ms.png)

### 1. Pasang Sambungan

Untuk memasang sambungan, taip nama sambungan dalam medan carian dan klik padanya untuk melihat maklumat tambahan tentang sambungan tersebut di kawasan kod setelah ia muncul di _activity bar_ yang diperluas.

Anda boleh klik butang _install biru_ pada _activity bar_ yang diperluas untuk memasang atau gunakan butang pasang yang muncul di kawasan kod setelah anda memilih sambungan untuk memuatkan maklumat tambahan.

![Install extensions](../../../../8-code-editor/images/install-extension.gif)

### 2. Sesuaikan Sambungan

Setelah memasang sambungan, anda mungkin perlu mengubah tingkah lakunya dan menyesuaikannya berdasarkan keutamaan anda. Untuk melakukan ini, pilih ikon Extensions, dan kali ini, sambungan anda akan muncul dalam folder _Installed_, klik pada ikon _**Gear**_ dan navigasi ke _Extensions Setting_.

![Modify extension settings](../../../../translated_images/extension-settings.21c752ae4f4cdb78a867f140ccd0680e04619d0c44bb4afb26373e54b829d934.ms.png)

### 3. Urus Sambungan

Setelah memasang dan menggunakan sambungan anda, vscode.dev menawarkan pilihan untuk mengurus sambungan anda berdasarkan keperluan yang berbeza. Sebagai contoh, anda boleh memilih untuk:

- **Disable:** _(Anda boleh melumpuhkan sambungan buat sementara waktu apabila anda tidak lagi memerlukannya tetapi tidak mahu menyahpasangnya sepenuhnya)_

    Pilih sambungan yang dipasang pada _activity bar_ yang diperluas > klik ikon Gear > pilih 'Disable' atau 'Disable (Workspace)' **ATAU** Buka sambungan pada kawasan kod dan klik butang Disable biru.

- **Uninstall:** Pilih sambungan yang dipasang pada _activity bar_ yang diperluas > klik ikon Gear > pilih 'Uninstall' **ATAU** Buka sambungan pada kawasan kod dan klik butang Uninstall biru.

---

## Tugasan

[Cipta laman web resume menggunakan vscode.dev](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/8-code-editor/1-using-a-code-editor/assignment.md)

## Kajian & Pembelajaran Kendiri

Baca lebih lanjut tentang [VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) dan beberapa ciri lain yang ditawarkannya.

---

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan perkhidmatan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Walaupun kami berusaha untuk memastikan ketepatan, sila ambil maklum bahawa terjemahan automatik mungkin mengandungi kesilapan atau ketidaktepatan. Dokumen asal dalam bahasa asalnya harus dianggap sebagai sumber yang berwibawa. Untuk maklumat penting, terjemahan manusia profesional adalah disyorkan. Kami tidak bertanggungjawab atas sebarang salah faham atau salah tafsir yang timbul daripada penggunaan terjemahan ini.