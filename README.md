<p align="justify"><b>Market Basket Analysis (MBA)</b> adalah teknik analisa yang digunakan oleh bisnis di bidang ritel untuk mencari asosiasi produk yang kuat, atau dengan kata lain menemukan paket produk yang bisa berdampak besar pada penjualan.
Algoritma yang bisa digunakan di R untuk melakukan MBA ini adalah apriori dari package arules. Data yang diperlukan hanya dua, yaitu data transaksi dan data produk.</p>
<p align="justify">Anda mungkin sering mendengar mengenai bagaimana banyak bisnis berkembang dan maju dengan cepat karena inovasi, baik itu inovasi di sisi produk ataupun bisnis.
<ol>Salah satu inovasi bisnis di bidang ritel adalah mencari asosiasi atau hubungan antar produk dari data transaksi penjualan yang bertujuan untuk: 
<li>dipaketkan dan dijual bersamaan.</li>
<li>memberikan rekomendasi produk kepada seseorang.</li>
<li>menyusun rak display.</li>
  <li>menyusun halaman produk e-commerce.</li></ol></p>
Semua hal ini bertujuan untuk meningkatkan penjualan sekaligus memecahkan masalah inventory – karena produk yang tidak begitu laku jika dipasangkan dengan tepat akan lebih menarik dan punya kemungkinan besar dibeli dalam satu paket. Proses ini merupakan proses analisa yang disebut dengan Market Basket Analysis (MBA). </p>
<details>
  <summary><b>Contoh Code Market Basket Analysis di R</b></br>#Menggunakan library arules</br>
library(arules)</br>
#Membaca transaksi dari file data_transaksi.txt</br>
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)</br>
#Menampilkan data transaksi dengan print dan inspect </br>
inspect(transaksi)</br>
#Menghasilkan model Market Basket Analysis</br>
mba <- apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))</br>
#Menampilkan paket produk</br>
inspect(subset(mba, lift>1))
</summary>
  <table border="0"><tr><td>inspect(subset(mba, lift>1))</br>
    lhs                     rhs        support confidence lift    </br>
[1] {Pet Food}           => {Sirup}    0.4     0.8000000  1.333333</br>
[2] {Sirup}              => {Pet Food} 0.4     0.6666667  1.333333</br>
[3] {Gula,Pet Food}      => {Sirup}    0.1     1.0000000  1.666667</br>
[4] {Pet Food,Teh Celup} => {Sirup}    0.2     0.6666667  1.111111</td></tr></table>
</details>

<details>
  <summary><b>Menampilkan Kombinasi dari Contoh Transaksi "Kecil"</b></br>#Menggunakan library arules</br>
library(arules)</br>
#Membaca transaksi dari file data_transaksi.txt</br>
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)</br>
#Menampilkan jumlah kombinasi dari produk yang terdapat pada daftar transaksi yang ada</br>
inspect(apriori(transaksi, parameter = list(support=.1, minlen=2, target='frequent itemsets')))
</summary>
  <table border="0"><tr><td>   items                      support</br>
[1] {Gula,Pet Food}            0.1    </br>
[2] {Gula,Sirup}               0.2    </br>
[3] {Gula,Teh Celup}           0.3    </br>
[4] {Pet Food,Sirup}           0.4    </br>
[5] {Pet Food,Teh Celup}       0.3    </br>
[6] {Sirup,Teh Celup}          0.4    </br>
[7] {Gula,Pet Food,Sirup}      0.1    </br>
[8] {Gula,Sirup,Teh Celup}     0.1    </br>
[9] {Pet Food,Sirup,Teh Celup} 0.2    </td></tr></table>
</details>

<details>
  <summary><b>Menampilkan Kombinasi dari Transaksi "Besar"</b></br>#Menggunakan library arules</br>
library(arules)</br>
#Membaca transaksi dari file data_transaksi2.txt</br>
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi2.txt", format="single", sep="\t", cols=c(1,2), skip=1)</br>
#Menampilkan jumlah kombinasi dari produk yang terdapat pada daftar transaksi yang ada</br>
inspect(apriori(transaksi, parameter = list(support=.03, minlen=2, target='frequent itemsets')))
</summary>
  <table border="0"><tr><td>items                              support</br>
[1]    {Shampo Biasa,    </br>                        
        Tas Makeup}                         0.031</br>
[2]    {Tank Top,        </br>                        
        Tas Tangan}                         0.032</br>
[3]    {Celana Pendek Jeans,    </br>                 
        Tas Tangan}                         0.031</br>
[4]    {Cover Koper,             </br>                
        Tas Tangan}                         0.030</br>
[5]    {Baju Batik Wanita,         </br>              
        Celana Panjang Format Hitam}        0.037</br>
...</br>
[1246] {Baju Batik Wanita,       </br>                
        Blouse Denim,             </br>               
        Sepatu Sandal Anak,        </br></br>              
        Serum Vitamin,             </br>              
        Shampo Biasa}                       0.031</br>
[1247] {Baju Batik Wanita,           </br>            
        Baju Kemeja Putih,           </br>            
        Sepatu Sandal Anak,          </br>            
        Serum Vitamin,                </br>           
        Shampo Biasa}                       0.030</br>
[1248] {Atasan Kaos Putih,                 </br>      
        Baju Renang Pria Dewasa,           </br>      
        Gembok Koper,                        </br>    
        Tank Top,                             </br>   
        Tas Travel,                           </br>   
        Wedges Hitam}                       0.044</td></tr></table>
</details>

Algoritma apriori adalah salah satu algoritma yang merupakan penerapan praktis dari Market Basket Analysis (MBA). Algoritma ini digunakan untuk menganalisa banyaknya kombinasi produk yang terjadi di dalam transaksi ritel, yang akan sulit dan lama jika dilakukan secara manual.

Secara teknis, algoritma apriori akan mencari tingkat asosiasi antar item di dalam banyak kombinasi kelompok data secara otomatis. Kombinasi ini juga bisa disusun dengan suatu aturan (rule) asosiasi "Jika membeli ini produk A maka akan membeli produk B", sehingga algoritma ini dikategorikan sebagai Association Rules di ranah machine learning.

Dengan menemukan paket produk yang asosiasinya kuat, Anda sebagai seorang data scientist dapat menyarankan kepada bisnis dapat melakukan berbagai action item seperti membuat paket produk dengan penawaran khusus, mendekatkan produk-produk tersebut saling berdekatan dalam satu rak, mengeluarkan rekomendasi produk di sistem e-commerce, mengurangi masalah stok, dan lain-lain.

Kesimpulan
Anda telah menyelesaikan bab yang berisi konsep-konsep fundamental yang sangat penting mengenai item, itemset dan rule. Mari kita review konsep dan contohnya dengan tampilan output berikut.

    lhs                     rhs        support confidence lift    
[1] {Pet Food}           => {Sirup}    0.4     0.8000000  1.333333
[2] {Sirup}              => {Pet Food} 0.4     0.6666667  1.333333
[3] {Gula,Pet Food}      => {Sirup}    0.1     1.0000000  1.666667
[4] {Pet Food,Teh Celup} => {Sirup}    0.2     0.6666667  1.111111
Item adalah produk tunggal yang terdapat dalam suatu transaksi.
Contoh: Pet Food, Sirup, Gula, dan Teh Celup.
Itemset adalah kombinasi satu atau lebih item yang terdapat dalam satu transaksi.
Contoh: {Pet Food}, {Gula, Pet Food}, {Sirup}, dan lain-lain. 
Rule adalah pernyataan hubungan antar Itemset. Biasanya dapat diformulasikan menjadi "Jika membeli itemset A, maka akan membeli itemset B".
Contoh: {Pet Food} => {Sirup}, {Pet Food, Teh Celup} => {Sirup}, dan lain-lain. 

### Membaca File sebagai Data Frame
Berikut adalah keterangan per bagian dari perintah tersebut:
transaksi_tabular: nama variable yang digunakan untuk menampung data dari contoh dataset
csv: function yang digunakan untuk membaca contoh dataset yang berupa file
https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt: lokasi dataset yang terdapat di web DQLab. Jika lokasi file dan aplikasi R terdapat di komputer lokal Anda, maka gantilah dengan lokasi file di lokal. Misalkan c:\data\data_transaksi.txt
sep: separator character atau karakter pemisah antar kolom, untuk file ini karakter pemisahnya adalah tab atau dalam notasi di R ditulis dengan "\t".

#Membaca file yang berlokasi di https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt dengan fungsi read.csv, dan kemudian disimpan pada variable transaksi_tabular
transaksi_tabular <- read.csv("https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", sep="\t")
#Menampilkan variable transaksi_tabular dengan fungsi print
print(transaksi_tabular)

Kode.Transaksi      Item
1             #01 Teh Celup
2             #01     Sirup
3             #01  Pet Food
4             #02 Teh Celup
5             #02      Gula
6             #03     Sirup
7             #03  Pet Food
8             #04 Teh Celup
9             #04     Sirup
10            #05 Teh Celup
11            #05     Sirup
12            #05      Gula
13            #06 Teh Celup
14            #06  Pet Food
15            #07 Teh Celup
16            #07     Sirup
17            #07  Pet Food
18            #08 Teh Celup
19            #09 Teh Celup
20            #09      Gula
21            #10     Sirup
22            #10  Pet Food
23            #10      Gula

### Membaca File sebagai Transaction
Keterangan code:

File : Parameter lokasi file yang bisa berasal dari url di web satau lokal. Pada contoh ini dibaca file data_transaksi.txt yang berlokasi di website academy.dqlab.id.
https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt: lokasi dataset yang terdapat di web DQLab. Jika lokasi file dan aplikasi R terdapat di komputer lokal Anda, maka gantilah dengan lokasi file di lokal. Misalkan c:\data\data_transaksi.txt
format: Format bisa "single" atau "basket".
"single" artinya tiap item transaksi dituliskan terpisah baris demi baris, dan ini cocok dengan format dari file kita.
"basket" artinya seluruh item per transaksi ditulis per baris.
sep: separator character atau karakter pemisah antar kolom, untuk file ini karakter pemisahnya adalah tab atau dalam notasi di R ditulis dengan "\t".
cols: indeks dari kolom-kolom yang digunakan. Untuk format single maka kolom harus dua saja, kolom pertama adalah kode transaksi sedangkan kolom kedua menunjukkan item transaksi. Penulisan c(1,2) pada contoh kita artinya kolom pertama dan kedua yang kita gunakan.
skip: jumlah baris yang dilewati sebelum mulai membaca data. Untuk dataset kita, baris pertama adalah header dan tidak diperlukan, jadi kita masukkan 1 sebagai input.

Keterangan hasil:
transactions in sparse format: Ini artinya transaksi dalam bentuk sparse (tersebar). Ini mungkin akan lebih jelas ketika divisualiasikan dalam bentuk matrix, ini akan kita praktekkan pada beberapa subbab di depan.
10 transactions (rows): dataset kita secara total memiliki 10 transaksi. Ada informasi rows atau baris disini, ini bukan berarti data kita ada 10 baris di file kita. Karena pada kenyataannya, file memiliki 23 baris data. 
4 items (kolom): dataset kita secara total memiliki 4 item unik.


library(arules)
read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)

output :
transactions in sparse format with
 10 transactions (rows) and
 4 items (columns)
 
 ### Menampilkan Daftar Item Transaksi
 Item-item yang terdapat pada objek transactions dapat dilihat pada komponen itemInfo dengan didahului aksesor @, jadi ditulis @iteminfo. Ini bermanfaat untuk melihat daftar unik item yang terdapat pada data transaksi yang sedang kita analisa. 
Mari kita praktekkan untuk lebih jelasnya, pada code editor kita terlihat potongan code dimana hasil read.transactions disimpan dalam sebuah variable bernama transaksi. 
 
 library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
transaksi@itemInfo

 | | labels|
 | :--: | --:|
|1  |    Gula|
|2 | Pet Food|
|3 |   Sirup|
|4| Teh Celup|

 
### Menampilkan Daftar Kode Transaksi
Sepuluh transaksi yang telah dibaca oleh read.transactions dapat dilihat detil kode-kodenya dengan menggunakan komponen itemsetInfo dengan aksesor @, atau lengkapnya ditulis dengan @itemsetInfo. Daftar ini bisa bermanfaat sebagai basis untuk menganalisa atau melakukan validasi dengan data yang ada pada sistem ritel.
Menyambung praktek sebelumnya, berikut adalah contoh penulisan untuk mengakses daftar kode transaksi dari variable transaksi.

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
transaksi@itemsetInfo

| |transactionID|
 | :--: | --:|
|1 |         |  #01|
|2|          |  #02|
|3  |         | #03|
|4 |          | #04|
|5 |          | #05|
|6 |          | #06|
|7  |         | #07
|8  |        |  #08|
|9  |         | #09|
|10  |        |#10|

### Tampilan Transaksi dalam bentuk Matrix

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
transaksi@data

4 x 10 sparse Matrix of class "ngCMatrix"                       
[1,] . | . . | . . . | |
[2,] | . | . . | | . . |
[3,] | . | | | . | . . |
[4,] | | . | | | | | | .

### Item Frequency
Setelah mengetahui bagaimana caranya menampilkan informasi daftar transaksi, kode transaksi, item dan distribusi item pada transaksi, kita harusnya ingin juga mengetahui item dengan jumlah kemunculannnya pada keseluruhan transaksi. Informasi ini disebut sebagai item frequency.
Untuk menghasilkan informasi ini kita gunakan fungsi itemFrequency dengan input objek transaction, dan hasilnya berupa named vector atau vector yang bisa diakses dengan nama.


library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
itemFrequency(transaksi, type="absolute")

itemFrequency(transaksi, type="absolute")
     Gula  Pet Food     Sirup Teh Celup 
        4         5         6         8 

### Statistik Top 3
Statistik sederhana untuk menjawab pertanyaaan seperti "Mana 3 item yang memiliki jumlah terbanyak di seluruh transaksi?" tidak bisa langsung dilakukan dengan satu fungsi di R, tapi perlu penggabungan beberapa perintah dimana salah satunya adalah fungsi sort.

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
data_item <- itemFrequency(transaksi, type="absolute")
#Melakukan sorting pada data_item
data_item <- sort(data_item, decreasing = TRUE)
#Mengambil 3 item pertama
data_item <- data_item[1:3]
#Konversi data_item menjadi data frame dengan kolom Nama_Produk dan Jumlah
data_item <- data.frame("Nama Produk"=names(data_item), "Jumlah"=data_item, row.names=NULL)
print(data_item)

  print(data_item)
   Nama.Produk   Jumlah
1   Teh Celup      8
2       Sirup      6
3    Pet Food      5

### Output Statistik Top 3 Sebagai File
 
Selain sebagai tampilan pada console, output dari sistem DQLab dapat berupa file. Dalam kesempatan kali ini, kita akan praktekkan bagaimana membuat file output untuk statistik top 3.

Dari hasil sebelumnya, kita sudah mendapatkan statistik top 3 dari jumlah item terbanyak dalam bentuk data frame. Ini bisa kita tuliskan langsung menggunakan fungsi write.csv, selengkapnya adalah sebagai berikut.

write.csv(data_item, file="top3_item_retail.txt", eol = "\r\n")
Disini kita menulis variable data_item ke dalam file bernama "top_3_item.retail.txt" yang diisikan ke dalam parameter file. Terdapat tambahan parameter eol = "\r\n", yang berguna untuk menghasilkan file yang bisa ditampilkan di Windows dengan baik.

Catatan: parameter terakhir ini bisa Anda abaikan pada saat mengerjakan proyek yang ada di DQLab.

Masukkan perintah tersebut ke dalam code editor untuk menggantikan bagian #[...1...] kemudian jalankan. Jika berhasil maka output console akan kosong, hanya menampilkan eksekusi perintah tersebut.

> write.csv(data_item, file="top3_item_retail.txt", eol = "\r\n") 
Namun jangan kuatir, karena output-nya berupa file. Klik tombol "Download Output File" seperti ditunjukkan pada gambar berikut.
download.png
 
Akan muncul window "List Output Files", carilah file bernama "top3_item_retail.txt" dan klik nama file tersebut untuk diunduh (download).
download (1).png


Buka file yang didownload tersebut dengan notepad, jika berhasil maka tampilannya terlihat sebagai berikut.
download (2).png

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
data_item <- itemFrequency(transaksi, type="absolute")
#Melakukan sorting pada data_item
data_item <- sort(data_item, decreasing = TRUE)
#Mengambil 3 item pertama
data_item <- data_item[1:3]
#Konversi data_item menjadi data frame dengan kolom Nama_Produk dan Jumlah
data_item <- data.frame("Nama Produk"=names(data_item), "Jumlah"=data_item, row.names=NULL)
#Menulis File Statistik Top 3
write.csv(data_item, file="top3_item_retail.txt", eol = "\r\n")

### Grafik Item Frequency
Selain tampilan transaksi dalam bentuk matrix, kita bisa juga melihat distribusi transaksi dari tiap item dalam bentuk grafik dengan menggunakan fungsi itemFrequencyPlot.
Perintahnya sederhana, seperti terlihat pada contoh berikut dimana kita plot distribusi dari dataset kita.

library(arules)
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
# Tampilan item frequency plot
itemFrequencyPlot(transaksi)	

grafikItemFreq.png


### Melihat Itemset per Transaksi dengan Inspect
Untuk melihat notasi itemset yang lebih baik dan mudah dimengerti kita bisa menggunakan function inspect. 

library(arules)
inspect(transaksi)

items                      transactionID
[1]  {Pet Food,Sirup,Teh Celup} #01          
[2]  {Gula,Teh Celup}           #02          
[3]  {Pet Food,Sirup}           #03          
[4]  {Sirup,Teh Celup}          #04          
[5]  {Gula,Sirup,Teh Celup}     #05          
[6]  {Pet Food,Teh Celup}       #06          
[7]  {Pet Food,Sirup,Teh Celup} #07          
[8]  {Teh Celup}                #08          
[9]  {Gula,Teh Celup}           #09          
[10] {Gula,Pet Food,Sirup}      #10          

### Menghasilkan Rules dengan Apriori
library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
#Menghasilkan associaton rules
apriori(transaksi)

### Melihat Rules dengan fungsi inspect
melihat daftar transaksi dengan menggunakan fungsi inspect. Selain transaksi, fungsi ini bisa digunakan juga untuk melihat isi dari association rules yang dihasilkan oleh fungsi apriori. Perhatikan pada code editor, hasil eksekusi apriori berupa rules sudah disimpan dalam variable bernama mba. 

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
#Menghasilkan association rules dan disimpan sebagai variable mba
mba <- apriori(transaksi)
#Melihat isi dari rules dengan menggunakan fungsi inspect
inspect(mba)

    lhs                rhs         support confidence lift    
[1] {}              => {Teh Celup} 0.8     0.8        1.000000
[2] {Pet Food}      => {Sirup}     0.4     0.8        1.333333
[3] {Gula,Pet Food} => {Sirup}     0.1     1.0        1.666667

### Filter RHS

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
#Menghasilkan association rules dan disimpan sebagai variable mba
mba <- apriori(transaksi)
#Filter rhs dengan item "Sirup" dan tampilkan
inspect(subset(mba, rhs %in% "Sirup"))

     lhs                rhs     support confidence lift    
[1] {Pet Food}      => {Sirup} 0.4     0.8        1.333333
[2] {Gula,Pet Food} => {Sirup} 0.1     1.0        1.666667

### Filter LHS
Filter dari praktek sebelumnya hanya berfokus kepada rhs, tentunya bisa juga dengan lhs.
Berikut adalah contoh perintah inspect untuk filter lhs dengan item Gula.
inspect(subset(mba, lhs %in% "Gula"))

library(arules)
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
mba <- apriori(transaksi)
inspect(subset(mba, lhs %in% "Gula"))

lhs                rhs     support confidence lift    
[1] {Gula,Pet Food} => {Sirup} 0.1     1          1.666667

### Filter LHS dan RHS
Berikut adalah contoh perintah inspect untuk filter lhs dengan item Pet Food dan rhs dengan item Sirup.
inspect(subset(mba, lhs %in% "Pet Food" & rhs %in% "Sirup"))

library(arules)
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
mba <- apriori(transaksi)
inspect(subset(mba, lhs %in% "Pet Food" & rhs %in% "Sirup"))

 lhs                rhs     support confidence lift    
[1] {Pet Food}      => {Sirup} 0.4     0.8        1.333333
[2] {Gula,Pet Food} => {Sirup} 0.1     1.0        1.666667 

### Menghasilkan Rules dengan Parameter Support dan Confidence
Berikut adalah perintah untuk menghasilkan kembali association rules dengan function apriori, tapi kali ini dengan tambahan parameter minimum support dan confidence masing-masing bernilai 0.1 dan 0.5.
apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))
Tugas Praktek
Tambahkan perintah pada code editor untuk menghasilkan rule dengan tingkat support minimum 0.1 dan minimum confidence 0.5.

source coding :

library(arules)
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))

Apriori

Parameter specification:
 confidence minval smax arem  aval originalSupport maxtime support minlen
        0.5    0.1    1 none FALSE            TRUE       5     0.1      1
 maxlen target   ext
     10  rules FALSE

Algorithmic control:
 filter tree heap memopt load sort verbose
    0.1 TRUE TRUE  FALSE TRUE    2    TRUE

Absolute minimum support count: 1 

set item appearances ...[0 item(s)] done [0.00s].
set transactions ...[4 item(s), 10 transaction(s)] done [0.00s].
sorting and recoding items ... [4 item(s)] done [0.00s].
creating transaction tree ... done [0.00s].
checking subsets of size 1 2 3 done [0.00s].
writing ... [16 rule(s)] done [0.00s].
creating S4 object  ... done [0.00s].
set of 16 rules 

### Inspeksi Rules Yang Dihasilkan
Tambahkan perintah pada code editor untuk menyimpan association rules ke dalam variable mba dan tampilkan isinya dengan function inspect.

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))
inspect(mba)


    lhs                rhs         support confidence lift    
[1] {}              => {Teh Celup} 0.8     0.8        1.000000
[2] {Pet Food}      => {Sirup}     0.4     0.8        1.333333
[3] {Gula,Pet Food} => {Sirup}     0.1     1.0        1.666667

### Filter LHS dan RHS (2)
Dengan 16 rules yang dihasilkan, kita bisa memiliki lebih banyak pilihan untuk melakukan filter lhs dan rhs seperti yang telah ditunjukkan pada bab Itemset and Rules.
Berikut adalah contoh untuk filter dimana lhs atau rhs keduanya memiliki item Teh Celup.
subset(mba, lhs %in% "Teh Celup" | rhs %in% "Teh Celup")

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
mba <- apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))
inspect(subset(mba, lhs %in% "Teh Celup" | rhs %in% "Teh Celup"))

lhs                     rhs         support confidence lift     
[1] {}                   => {Teh Celup} 0.8     0.8000000  1.0000000
[2] {Gula}               => {Teh Celup} 0.3     0.7500000  0.9375000
[3] {Pet Food}           => {Teh Celup} 0.3     0.6000000  0.7500000
[4] {Sirup}              => {Teh Celup} 0.4     0.6666667  0.8333333
[5] {Teh Celup}          => {Sirup}     0.4     0.5000000  0.8333333
[6] {Gula,Sirup}         => {Teh Celup} 0.1     0.5000000  0.6250000
[7] {Pet Food,Sirup}     => {Teh Celup} 0.2     0.5000000  0.6250000
[8] {Pet Food,Teh Celup} => {Sirup}     0.2     0.6666667  1.1111111
[9] {Sirup,Teh Celup}    => {Pet Food}  0.2     0.5000000  1.0000000

### Filter berdasarkan Lift
Sebagai contoh, untuk melakukan filter terhadap objek mba dengan kondisi berikut:
lhs atau rhs memiliki Teh Celup
lift di atas 1

maka perintahnya adalah sebagai berikut
subset(mba, (lhs %in% "Teh Celup" | rhs %in% "Teh Celup") & lift>1)

library(arules)
transaksi <- read.transactions(file="https://storage.googleapis.com/dqlab-dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
mba <- apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))
inspect(subset(mba, (lhs %in% "Teh Celup" | rhs %in% "Teh Celup") & lift>1))

      lhs                     rhs     support confidence lift    
[1] {Pet Food,Teh Celup} => {Sirup} 0.2     0.6666667  1.111111


### Rekomendasi - Filter dengan %ain%
Operator %in% yang sebelumnya kita gunakan sudah efektif. Namun operator ini tidak cocok jika kita ingin melakukan filter itemset dengan logika AND. Artinya seluruh item harus muncul dalam itemset yang terpilih. Untuk keperluan tersebut, gunakan operator %ain%.

Contoh subset yang menggunakan %ain% adalah sebagai berikut.
subset(mba, (lhs %ain% c("Pet Food", "Gula" )))

library(arules)
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
mba <- apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))
inspect(subset(mba, (lhs %ain% c("Pet Food", "Gula"))))


 lhs                rhs     support confidence lift    
[1] {Gula,Pet Food} => {Sirup} 0.1     1          1.666667


### Visualisasi Rules dengan Graph
Perhatikan fungsi plot ini merupakan pengembangan dari package arules. Method graph menunjukkan bahwa plot ini harus menghasilkan visualisasi dengan tipe jaringan.

library(arules)
library(arulesViz)
transaksi <- read.transactions(file="https://academy.dqlab.id/dataset/data_transaksi.txt", format="single", sep="\t", cols=c(1,2), skip=1)
mba <- apriori(transaksi,parameter = list(supp = 0.1, confidence = 0.5))
plot(subset(mba, lift>1.1), method="graph")

download (3).png

