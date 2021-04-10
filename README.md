<p align="justify"><b>Market Basket Analysis (MBA)</b> adalah teknik analisa yang digunakan oleh bisnis di bidang ritel untuk mencari asosiasi produk yang kuat, atau dengan kata lain menemukan paket produk yang bisa berdampak besar pada penjualan.
Algoritma yang bisa digunakan di R untuk melakukan MBA ini adalah apriori dari package arules. Data yang diperlukan hanya dua, yaitu data transaksi dan data produk.</p>
<p align="justify">Anda mungkin sering mendengar mengenai bagaimana banyak bisnis berkembang dan maju dengan cepat karena inovasi, baik itu inovasi di sisi produk ataupun bisnis.
<ol>Salah satu inovasi bisnis di bidang ritel adalah mencari asosiasi atau hubungan antar produk dari data transaksi penjualan yang bertujuan untuk: 
<li>dipaketkan dan dijual bersamaan.</li>
<li>memberikan rekomendasi produk kepada seseorang.</li>
<li>menyusun rak display.</li>
<li>menyusun halaman produk e-commerce.</li></ol?
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
