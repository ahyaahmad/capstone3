# capstone3
Capstone Project Module 3: Churn Analysis on E-Commerce Dataset 
### Background

Sebuah perusahaan E-Commerce melakukan analisa terhadap perkembangan bisnis mereka dan menemukan bahwa salah satu tantangan yang dihadapi adalah pelanggan yang melakukan Churn (berhenti melakukan transaksi).

Apa itu customer churn?
Customer churn adalah metrik bisnis yang mengukur jumlah pelanggan yang telah berhenti menggunakan produk atau layanan Anda. Ketika perusahaan mampu mengurangi atau mencegah customer churn , mereka dapat meningkatkan customer lifetime value (CLV). CLV adalah jumlah total uang yang dapat Anda harapkan dari rata-rata pelanggan untuk dibelanjakan dengan bisnis Anda selama masa hidup mereka.

Jauh lebih murah bagi perusahaan untuk mempertahankan basis pelanggan mereka saat ini daripada menghabiskan sumber daya untuk mendapatkan pelanggan baru. Oleh karena itu, mengeksplorasi strategi untuk mengurangi dan mencegah customer churn  dapat menjadi cara yang bagus untuk meningkatkan profitabilitas perusahaan.

Sebagai konteks, ada dua cara agar perusahaan dapat mempertahankan profitabilitas perusahaan. Pertama yaitu mempertahankan customer lama agar menetap sebagai customer. Cara kedua yaitu mencari customer baru. Berdasarkan statistik dari berbagai industri bisnis, hasil riset menemukan bahwa customer acquisition memiliki biaya 4-5x lipat lebih dari customer retention

Untuk memberikan gambaran konsekuensi secara kuantitatif, maka kita akan coba hitung dampak biaya berdasarkan asumsi berikut :
- Customer Lifetime Period untuk pelanggan yang churn sekitar 17.7 bulan 
- Customer Acquisition Cost (CAC) = 315 USD per customer ([sumber](https://www.revechat.com/blog/customer-acquisition-cost/)) / 17.7 bulan = 17.79 USD per bulan per customer
- Customer Retention Cost (CRC)= 1/5 ([sumber](https://www.outboundengine.com/blog/customer-retention-marketing-vs-customer-acquisition-marketing/)) * CAC = 1/5 * 17.79 USD = 3.56 USD per bulan per customer
- Average Customer MonthlyCharge = 64.88 USD per bulan per customer

Berdasarkan asumsi di atas maka kita dapat coba kuantifikasi konsekuensinya sebagai berikut :
- tidak efektifnya pemberian insentif retensi --> maka kita menyia-nyiakan biaya CRC sebesar 3.56 USD per bulan per pelanggan
- kehilangan pelanggan --> maka kita kehilangan pendapatan dan juga perlu mengeluarkan kembali biaya CAC sehingga secara total kita kehilangan 17.79 USD + 64.88 USD = 82.67 USD per bulan per pelanggan

Dengan demikian, bagi perusahaan E-Commerce untuk mendapatkan customer baru menghabiskan biaya yang lebih banyak dibandingkan dengan mempertahankan customer lama untuk tidak churn sehingga kita harus lebih fokus ke customer retention. Sehingga, perusahaan harus memikirkan cara untuk memprediksi customer yang berpotensi untuk churn dan memberikan treatment yang diperlukan agar customer menetap di platform E-Commerce perusahaan.

### Problem Statement

Tingginya persentase customer churn menjadi salah satu indikator tingkat kegagalan suatu perusahaan E-Commerce, maka perlu dilakukan upaya-upaya untuk mengurangi persentase customer churn tersebut. Perusahaan umumnya lebih memilih untuk mempertahankan pelanggan, karena dibutuhkan biaya yang lebih sedikit untuk mempertahankan pelanggan (customer retention cost) daripada menambah pelanggan yang baru (customer acquisition cost). Berdasarkan informasi dari [internet](https://www.outboundengine.com/blog/customer-retention-marketing-vs-customer-acquisition-marketing/), memperoleh pelanggan baru dapat menghabiskan biaya lima kali lebih banyak daripada mempertahankan pelanggan yang sudah ada.

Perusahaan E-Commerce dapat memberikan insentif retensi seperti memberikan Cashback (hadiah uang tunai), Discount (potongan harga), gratis ongkos kirim, memberikan paket layanan yang menarik, memberikan prioritas pelayanan dan lain-lain dalam upaya untuk mempertahankan pelanggan. Namun, kebijakan pemberian insentif retensi belum sepenuhnya dilakukan secara efektif. Karena jika insentif retensi tersebut diberikan secara merata kepada seluruh pelanggan, maka pengeluaran biaya tersebut menjadi tidak efektif dan mengurangi potensi keuntungan apabila pelanggan tersebut memang loyal dan tidak ingin berhenti berlangganan.

### Analytic Approach

Kita akan menganalisis data untuk menemukan pola yang membedakan customer yang akan churn atau yang tidak churn. Kemudian kita akan membangun model klasifikasi yang akan membantu perusahaan untuk dapat memprediksi customer akan churn atau tidak.

### Metric Evaluation

|       | N-Pred| P-Pred |
| --- | --- | --- |
| **N-Act**     | TP | FP |
| **P-Act**      | FN | TP |

Target:
- 0: customer tidak churn
- 1: customer churn

Confusion Metrix Term:
- TP: customernya aktualnya churn dan diprediksi churn
- TN: customernya aktualnya tidak churn dan diprediksi tidak churn
- FN: customernya aktualnya churn dan diprediksi tidak churn
- FP: customernya aktualnya tidak churn dan diprediksi churn

Cost FN (False Negative):
- Kekurangan
    - Kehilangan customer (alias churn)
    - Adanya cost customer acquistion untuk menggantikan customer yang telah churn   

Cost FP (False Positive):
- Kelebihan
    - Akibat dari salah treatment terhadap customer yang sebenarnya tidak churn tapi diprediksi churn, maka reputasi E-Commerce semakin baik (customer yang tidak churn akan mengira bahwa plaform E-Commerce murah hati untuk memberikan promo secara cuma-cuma)
    <br><br>
- Kekurangan
    - Salah target treatment untuk customer yang tidak churn (tapi diprediksi churn)
    - Sia-sianya biaya customer retention, waktu dan sumber daya

Dengan demikian, maka perusahaan berusaha untuk membuat model yang dapat mengurangi cost customer retention dari perusahaan tersebut tetapi tanpa harus ada customer yang churn dari website E-Commerce perusahaan. Oleh karena itu, kita memutuskan untuk menitikberatkan ke False Negative, tetapi juga tidak lupa dengan False Positive, dengan lebih menitikberatkan pada recall. Maka dari itu focus metric yang akan digunakan adalah **F2-Score**

### Summary

Tujuan dari project ini adalah untuk mengetahui prediksi seorang customer apakah akan melakukan churn atau tidak menggunakan jasa perusahaan e-commerce ini lagi. Berdasarkan business problem di atas, diketahui bahwa:

- model dapat mengetahui 93% pelanggan yang tidak churn dan 85% pelanggan yang churn (Berdasarkan Recall)
- Selain itu model memiliki kemungkinan prediksi benar untuk pelanggan yang akan churn sebesar 72%. Maka masih ada pelanggan yang churn dan diprediksi sebagai tidak churn sebesar 15%.

**Type 1 error** : False Positive  
Konsekuensi: [*operation loss*](https://www.investopedia.com/terms/o/operating-loss.asp#:~:text=An%20operating%20loss%20occurs%20when,profit%20before%20interest%20and%20taxes.) karena mengeluarkan biaya promo untuk pelanggan yang tidak tepat. biaya yang dikeluarkan sebesar 50 USD per customer bulan[source](https://sci-hub.se/https://doi.org/10.1016/j.jretconser.2017.10.007).

**Type 2 error** : False Negative  
Konsekuensi: *profit loss* karena customer *churn*. biaya yang dikeluarkan 5x lipat dari biaya promo ke customer 250 USD per customer per bulan[source](https://www.superoffice.com/blog/reduce-customer-churn/)

**Without Machine Learning**

Perusahaan e-commerce tidak dapat mengetahui customer yang akan melakukan churn, sehingga perusahaan e-commerce harus memberikan promosi ke semua customer, agar perusahaan tidak kehilangan customer. Ini menyebabkan perusahaan e-commerce harus mengeluarkan biaya yang besar dalam mengimplentasikan strategi promosinya. 

- Pengeluaran perusahaan untuk promosi ke semua customer 50 USD x 654 = 32.700 USD
- Promosi yang tepat sasaran pada orang yang churn: 250 USD X 107 = 26.750 USD

Sehingga diketahui bahwa perusahaan e-commerce mengeluarkan biaya yang tidak tepat sasaran (biaya promosi untuk customer yang loyal) sebesar: - 32.700 + 26.750 USD = **- 5.950 USD**. Karena 654 customer adalah 1/5 dari total customer (3.269) maka -5.950 USD x 5 = **-29.750 USD**. Biaya tersebut seharusnya dapat ditekan jika menggunakan Machine Learning

**With Machine Learning**

Biaya yang tidak tepat sasaran di atas, dapat ditekan jika menggunakan Machine Learning, dengan memprediksi customer yang akan melakukan churn. Sehingga biaya promosi dapat difokuskan kepada customer yang akan melakukan churn, berdasarkan dari hasil prediksi dari Machine Learning.

- Pengeluaran perusahaan e-commerce promosi yang diprediksi churn (FP+TP): (36+91) x 50 USD = 6.350 USD
- Perusahaan e-commerce kehilangan customer karena tidak terprediksi akan churn (FN): 16 x 250 USD = 4.000 USD
- Promosi tepat sasaran (TP): 91 x 250 USD = 22.750 USD

Sehingga diketahui bahwa perusahaan e-commerce berhasil menghasilkan Revenue per bulan sebesar: - 6.350 - 4.000 + 22.750 = **12.400 USD**. Karena 654 customer adalah 1/5 dari total customer (3.269) maka 12.400 USD x 5 = **62.000 USD**

**Comparison between using Machine Learning and not using Machine Learning**

- Sebelum pakai ML: perusahaan merugi **-29.750 USD** per bulan
- Setelah menggunakan ML: perusahaan berhasil menghasilkan profit **62.000 USD** per bulan

Dapat disimpulkan bahwa Machine Learning dengan menggunakan algoritma LightGBM setelah tuning dua kali berhasil menghasilkan profit **62.000** per bulan.

**The primary factors affecting customer churn**

Berdasarkan Feature Importance dan Summary Plot, 3 Faktor utama yang mempengaruhi prediksi Customer Churn secara berurutan adalah 
1. `Tenure`
  - Semakin kecil nilai `Tenure` artinya semakin baru customer berlangganan semakin besar kemungkinan Customer akan churn dan semakin lama customer berlangganan semakin betah dia terhadap layanan perusahaan. `Tenure` memiliki tingkat pengaruh lebih dari 300% dari `Complain`
2. `Complain`
  - Semakin besar nilai `Complain` semakin besar kemungkinan Customer akan Churn dan sebaliknya. nilai yang besar artinya customer melakukan complain atau customer tidak puas terhadap layanan.
3. `NumberOfAddress`
  - Semakin besar nilai `NumberOfAddress` semakin besar kemungkinan Customer akan Churn dan sebaliknya. nilai yang besar artinya alamat yang didaftarkan semakin banyak. Hal ini dimungkinkan jika Customer tersebut berpindah alamat.
