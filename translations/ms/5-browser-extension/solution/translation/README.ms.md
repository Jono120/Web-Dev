<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "21b364c158c8e4f698de65eeac16c9fe",
  "translation_date": "2025-08-27T22:26:57+00:00",
  "source_file": "5-browser-extension/solution/translation/README.ms.md",
  "language_code": "ms"
}
-->
# Sambungan Penyemak Imbas Carbon Trigger: Kod Lengkap

Menggunakan API Isyarat CO2 tmrow untuk memantau penggunaan elektrik, bina sambungan penyemak imbas supaya anda boleh menerima peringatan di penyemak imbas anda tentang tahap penggunaan elektrik di kawasan anda. Menggunakan sambungan ini secara khusus akan membantu anda membuat keputusan yang lebih bijak berdasarkan maklumat ini.

![tangkapan pelanjutan penyemak imbas](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.ms.png)

## Bermula Dari Sini

Anda perlu memasang [npm](https://npmjs.com). Muat turun salinan kod ini ke dalam folder di komputer anda.

Pasang semua pakej yang diperlukan:

```
npm install
```

Bina sambungan menggunakan webpack:

```
npm run build
```

Untuk memasang di Edge, gunakan menu 'tiga titik' di sudut kanan atas penyemak imbas untuk mencari panel Sambungan. Dari sana, pilih 'Load Unpacked' untuk memuatkan sambungan baru. Buka folder 'dist' apabila diminta, dan sambungan akan dimuatkan. Untuk menggunakannya, anda memerlukan kunci API untuk API Isyarat CO2 ([dapatkan satu di sini melalui e-mel](https://www.co2signal.com/) - masukkan e-mel anda di dalam kotak di halaman ini) dan [kod untuk wilayah anda](http://api.electricitymap.org/v3/zones) yang sesuai dengan [Peta Elektrik](https://www.electricitymap.org/map) (contohnya, di Boston, saya menggunakan 'US-NEISO').

![sedang memuat turun](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.ms.png)

Setelah kunci API dan wilayah dimasukkan ke dalam antara muka sambungan, titik berwarna di bar sambungan penyemak imbas akan berubah untuk mencerminkan penggunaan tenaga di kawasan anda dan memberikan cadangan mengenai aktiviti berat yang sesuai untuk dilakukan. Konsep di sebalik sistem 'dot' ini diilhamkan oleh [sambungan penyemak imbas Lollipop Tenaga](https://energylollipop.com/) untuk pelepasan di California.

---

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan perkhidmatan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Walaupun kami berusaha untuk memastikan ketepatan, sila ambil perhatian bahawa terjemahan automatik mungkin mengandungi kesilapan atau ketidaktepatan. Dokumen asal dalam bahasa asalnya harus dianggap sebagai sumber yang berwibawa. Untuk maklumat yang kritikal, terjemahan manusia profesional adalah disyorkan. Kami tidak bertanggungjawab atas sebarang salah faham atau salah tafsir yang timbul daripada penggunaan terjemahan ini.