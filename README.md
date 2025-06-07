# PROJECT-UAS-PENAMBANGAN-DATA-KELOMPOK-7
# Laporan Project Pengganti Uas Mata kuliah Penambangan Data ( Data Mining) - Prediksi Risiko Drop Out Mahasiswa
# Dosen Pengampu
1. Ir. Arie Vatresia, S.T., M.T.I., Ph.D
# Anggota Kelompok 7 
1. Fadlan Dwi Febrio  G1A022051
2. Arief Setiawan     G1A022055
3. Rengga Anggarah    G1A022069
# Domain Proyek
  Pendidikan tinggi merupakan investasi penting bagi individu dan masyarakat. Namun, fenomena mahasiswa drop out (DO) tetap menjadi tantangan besar bagi institusi pendidikan. Berdasarkan penelitian oleh UNESCO (2020), tingkat drop out mahasiswa di Indonesia mencapai 20-25% setiap tahunnya, dengan kerugian ekonomi diperkirakan mencapai triliunan rupiah. Masalah drop out tidak hanya berdampak finansial bagi mahasiswa dan keluarga, tetapi juga mempengaruhi reputasi institusi pendidikan. Penelitian oleh Tinto menunjukkan bahwa faktor akademik seperti IPK dan kehadiran kelas, serta faktor non-akademik seperti status pekerjaan dan kondisi ekonomi, berkontribusi signifikan terhadap keputusan mahasiswa untuk drop out. Sistem prediksi risiko drop out berbasis data mining dapat membantu universitas mengidentifikasi mahasiswa berisiko sejak dini, sehingga intervensi akademik yang tepat dapat diberikan. Model prediksi ini menggunakan data historis mahasiswa untuk memprediksi kemungkinan drop out dengan akurasi tinggi.
# Business Understanding
Problem Statements
1. Tingginya angka drop out mahasiswa menyebabkan kerugian finansial dan reputasi bagi universitas.
2. Kurangnya sistem deteksi dini untuk mengidentifikasi mahasiswa berisiko drop out.
3. Intervensi akademik seringkali terlambat diberikan karena ketiadaan alat prediksi yang akurat.

Goals
1. Mengembangkan model prediksi risiko drop out dengan akurasi minimal 90%.
2. Membantu universitas memberikan intervensi akademik lebih awal kepada mahasiswa berisiko.
3. Mengoptimalkan alokasi sumber daya untuk program retensi mahasiswa.

Solution statements
1. Mengimplementasikan algoritma Decision Tree karena kemampuannya menangani data campuran (numerik dan kategorikal) serta interpretasi model yang mudah.
2. Menerapkan teknik preprocessing data komprehensif termasuk handling missing value, normalisasi, dan encoding.
3. Menggunakan metrik evaluasi komprehensif (akurasi, precision, recall, F1-score) untuk memastikan model memiliki performa yang seimbang.
# Data Understanding
Dataset yang digunakan dalam proyek ini merupakan data dummy yang mensimulasikan karakteristik mahasiswa dengan variabel-variabel sebagai berikut:
1. ID: Identifikasi unik mahasiswa
2. IPK_Sem1 sampai IPK_Sem4: IPK mahasiswa per semester
3. Kehadiran_Rata: Rata-rata kehadiran mahasiswa
4. Remedial_Total: Jumlah mata kuliah yang diulang
5. Aktivitas_Online: Tingkat aktivitas di sistem pembelajaran daring
6. Pekerjaan: Status pekerjaan mahasiswa (Ya/Tidak)
7. Jam_Kerja_Mingguan: Beban kerja mingguan jika bekerja
8. Pendapatan_OrangTua: Tingkat pendapatan orang tua
9. Tanggungan_Keluarga: Jumlah tanggungan keluarga
10. Risiko_DO: Variabel target (1=Berisiko, 0=Aman)

Dataset terdiri dari 2000 entri dengan distribusi sebagai berikut:
1. IPK rata-rata berkisar 2.8-2.82 dengan standar deviasi 0.49-0.67
2. Rata-rata kehadiran 79.98% dengan standar deviasi 9.69
3. 13.05% mahasiswa termasuk dalam kategori berisiko DO

# Data Preparation
Proses data preparation yang dilakukan meliputi:
1. Exploratory Data Analysis:
   + Analisis statistik deskriptif untuk memahami distribusi data
   + Pengecekan missing value dan duplikat data
   + Analisis korelasi antar variabel
2. Preprocessing:
   + Penanganan missing value: Tidak ditemukan missing value pada dataset ini
   + Encoding variabel kategorikal menggunakan One-Hot Encoding untuk variabel 'Pekerjaan'
   + Normalisasi data numerik menggunakan Min-Max Scaler
   + Penghapusan variabel tidak relevan ('ID')
3. Pemisahan Data:
   + Pembagian dataset menjadi training set (80%) dan test set (20%)
   + Menggunakan stratified sampling untuk mempertahankan distribusi kelas target
     
Alasan preprocessing:
+ One-Hot Encoding dipilih karena variabel kategorikal hanya memiliki 2 nilai
+ Normalisasi penting untuk memastikan semua fitur memiliki skala yang sama
+ Stratified sampling menjaga proporsi kelas minoritas di kedua subset

# Modeling
Algoritma yang digunakan adalah Decision Tree dengan pertimbangan:
1. Kemampuan menangani data campuran (numerik dan kategorikal)
2. Hasil yang mudah diinterpretasikan oleh stakeholder non-teknis
3. Tidak memerlukan normalisasi data yang ekstensif
4. Cepat dalam pelatihan dan prediksi

Parameter model yang dioptimalkan:
+ max_depth=5: Membatasi kedalaman pohon untuk mencegah overfitting
+ random_state=42: Memastikan hasil yang reproducible

Proses pemodelan:
1. Inisialisasi model Decision Tree
2. Pelatihan model menggunakan data training
3. Evaluasi performa menggunakan data test

Kelebihan Decision Tree:
+ Mudah diinterpretasikan dan divisualisasikan
+ Tidak memerlukan normalisasi data
+ Cepat dalam pelatihan dan prediksi

Kekurangan Decision Tree:
+ Rentan terhadap overfitting jika tidak diatur dengan baik
+ Sensitif terhadap perubahan kecil dalam data

# Evaluation
1. Gambar hasil evaluasi model klasifikasi

    ![Akurasi model](https://github.com/user-attachments/assets/582a0da0-2605-40c3-a675-ccc7b892e1a5)
   
      Gambar di atas menampilkan hasil evaluasi model klasifikasi dengan akurasi sebesar 94.25%. Confusion Matrix menunjukkan model melakukan prediksi benar untuk kelas "Aman" (Kelas 0) sebanyak 343 instance (true negative) dan 5 instance salah prediksi (false positive), sedangkan untuk kelas "Risiko DO" (Kelas 1) benar sebanyak 34 instance (true positive) dan salah 18 instance (false negative). Laporan Klasifikasi (Classification Report) mengungkapkan bahwa kelas "Aman" memiliki precision 0.95, recall 0.99, dan f1-score 0.97, sementara kelas "Risiko DO" memiliki precision 0.87, recall 0.65, dan f1-score 0.75. Nilai macro avg dan weighted avg masing-masing adalah 0.86 dan 0.94 untuk f1-score, menunjukkan performa model yang baik secara keseluruhan meskipun recall untuk kelas minoritas ("Risiko DO") relatif lebih rendah. Data terdiri dari total 400 instance dengan 348 instance kelas "Aman" dan 52 instance kelas "Risiko DO".

  Interpretasi hasil:
  + Model menunjukkan performa sangat baik dengan akurasi 94.25%
  + Precision 0.87 untuk kelas berisiko menunjukkan 87% prediksi berisiko adalah benar
  + Recall 0.65 berarti model dapat mengidentifikasi 65% dari semua kasus berisiko
  + F1-score 0.75 menunjukkan keseimbangan antara precision dan recall


3. Gambar visualisasi pohon keputusan untuk prediksi risiko DO

     ![visualisasi pohon keputusan untuk prediksi risiko DO](https://github.com/user-attachments/assets/03fffb74-ac71-4991-955f-c86f62f53260)

   Gambar di atas menampilkan visualisasi pohon keputusan untuk memprediksi "Risiko DO" (Drop Out) berdasarkan beberapa fitur seperti Rm_Kerju_Hirogawa, Remedial_Total, Tinygwonga_Kekuaga, Pendapasim_Oompina, dan Kekadiruma_Rata. Setiap cabang pohon menunjukkan aturan pemisahan dengan nilai ambang batas (misal: <= 20.5), gini impurity (gm) yang mengukur ketidakmurnian split (semakin kecil semakin baik), jumlah sampel, distribusi kelas ([nilai Aman, nilai Risiko DO]), serta kelas prediksi akhir. Misalnya, jika Rm_Kerju_Hirogawa ≤ 20.5, model cenderung memprediksi "Aman" (nilai = [1.19, 9.7]). Beberapa cabang seperti Tinygwonga_Kekuaga ≤ 6.5 mengarah ke prediksi "Risiko DO" (nilai = [2.80, 9.6]), menunjukkan fitur ini berpengaruh signifikan. Struktur pohon yang berulang (misal: RmKerju_Rata dengan ambang batas 70-85) mengindikasikan bahwa fitur tersebut kurang berdampak pada prediksi. Secara keseluruhan, pohon ini menggambarkan logika model dalam mengklasifikasikan siswa berdasarkan kriteria akademik dan non-akademik.

  Visualisasi pohon keputusan membantu memahami faktor penentu risiko drop out:
  + IPK semester awal menjadi pembeda utama
  + Kehadiran dan jumlah remedial juga berpengaruh signifikan
  + Faktor pekerjaan dan beban kerja muncul di cabang-cabang berikutnya

4. Gambar sistem prediksi risiko dop out mahasiswa

   ![sistem prediksi risiko dop out mahasiswa](https://github.com/user-attachments/assets/4bff7fb2-0a43-4986-b0ff-1330399ca38f)

   Gambar di atas menampilkan antarmuka Sistem Prediksi Risiko Drop Out (DO) Mahasiswa yang memungkinkan pengguna memasukkan data akademik dan non-akademik mahasiswa untuk diprediksi. Contoh input menunjukkan mahasiswa dengan IPK rendah (2.0-2.5), kehadiran buruk (30%), remedial tinggi (10), aktivitas online rendah (3 jam/minggu), bekerja (30 jam/minggu), pendapatan orang tua rendah (2 juta/bulan), dan tanggungan keluarga besar (4), sehingga sistem memprediksi "BERISIKO DROP OUT" dengan probabilitas 100%. Sistem juga memberikan rekomendasi perbaikan seperti konsultasi dengan DPA, meningkatkan kehadiran, mengurangi remedial, mengatur jadwal kerja-kuliah, dan mencari bantuan finansial. Antarmuka ini bersifat interaktif, memungkinkan pengujian data baru, dan dirancang untuk membantu identifikasi dini mahasiswa berisiko DO beserta solusi penanganannya.

# development plan
1. Integrasi dengan sistem akademik untuk prediksi real-time

   Integrasi sistem prediksi dengan sistem akademik yang ada (seperti SIAKAD atau LMS) akan memungkinkan akses real-time terhadap data mahasiswa. Hal ini mencakup:
    + Automatisasi Input Data: Sistem akan terhubung langsung ke database akademik untuk mengambil data terbaru (IPK, kehadiran, remedial) secara berkala, mengurangi kesalahan manual dan memastikan prediksi selalu berdasarkan data terkini.
    + Sinkronisasi dengan Sistem Monitoring: Hasil prediksi akan otomatis terkirim ke dosen wali atau departemen akademik melalui notifikasi atau laporan terintegrasi. Misalnya, jika seorang mahasiswa terdeteksi berisiko DO, sistem dapat mengirimkan alert ke pihak terkait.
    + API untuk Interoperabilitas: Pengembangan API (Application Programming Interface) akan memfasilitasi pertukaran data antara sistem prediksi dan platform lain (e.g., sistem bimbingan akademik).
  
    Integrasi dengan sistem akademik merupakan langkah krusial untuk memastikan sistem prediksi dapat beroperasi secara efisien dan efektif. Dengan menghubungkan sistem ini ke SIAKAD atau LMS, data seperti IPK dan kehadiran akan diperbarui secara otomatis, menghilangkan kebutuhan input manual yang rentan error. Selain itu, integrasi memungkinkan tindakan cepat berdasarkan prediksi, seperti penjadwalan konseling atau penyesuaian beban SKS. API yang dikembangkan akan mendukung interoperabilitas dengan sistem lain, misalnya untuk mengirim rekomendasi intervensi ke sistem manajemen bimbingan akademik.
2. Pengembangan Dashboard Visualisasi

   Dashboard interaktif akan dirancang untuk memudahkan rektorat, fakultas, dan dosen memantau risiko DO secara visual. Fitur yang akan dikembangkan:
   + Visualisasi Tren Risiko: Grafik garis atau heatmap untuk menunjukkan tren risiko DO per semester/prodi.
   + Detail Mahasiswa Berisiko: Tabel yang memfilter mahasiswa berdasarkan tingkat risiko (rendah, sedang, tinggi) dengan informasi seperti alasan prediksi (contoh: IPK turun drastis, kehadiran rendah).
   + Drill-Down Analysis: Kemampuan mengeksplorasi data spesifik, seperti membandingkan faktor risiko antarprodi atau tahun akademik.
   + Ekspor Laporan: Opsi untuk menghasilkan laporan PDF/Excel berisi daftar mahasiswa berisiko beserta rekomendasi tindakan.
  
   Dashboard visualisasi akan menjadi antarmuka utama bagi pemangku kepentingan untuk memahami hasil prediksi. Dengan grafik interaktif, rektorat dapat mengidentifikasi pola risiko DO secara makro (misalnya, peningkatan risiko di prodi tertentu) dan mikro (kinerja individu mahasiswa). Fitur drill-down memungkinkan analisis mendalam, seperti melihat korelasi antara status pekerjaan dan risiko DO. Laporan yang dapat diekspor akan membantu fakultas merencanakan intervensi berbasis data, seperti program mentoring tambahan untuk mahasiswa dengan kehadiran rendah.
   
3. Peningkatan Model Prediksi
   + Penambahan Fitur Baru: Memasukkan variabel baru seperti partisipasi dalam kegiatan kampus atau kesehatan mental (melalui kuesioner).
   + Pemilihan Model yang Lebih Akurat: Eksperimen dengan algoritma lain (Random Forest, XGBoost) dan teknik tuning hyperparameter.
   + Validasi Berkala: Evaluasi model setiap semester menggunakan data terbaru untuk memastikan keakuratan tetap tinggi.
  
   Model saat ini menggunakan Decision Tree dengan akurasi 94.25%, namun pengembangan ke depan akan fokus pada peningkatan cakupan prediksi. Dengan menambahkan variabel seperti keterlibatan dalam organisasi mahasiswa atau data kuesioner kesehatan mental, sistem dapat menangkap faktor risiko yang sebelumnya terlewat. Uji coba algoritma lain seperti XGBoost mungkin memberikan akurasi lebih tinggi untuk data tidak seimbang (minoritas kelas risiko tinggi). Validasi berkala akan menjaga relevansi model seiring perubahan perilaku mahasiswa.
  
4. Pengembangan Fitur Tambahan
   + Sistem Early Warning: Notifikasi otomatis ke mahasiswa berisiko via email/sistem akademik, disertai saran tindakan.
   + Modul Intervensi: Rekomendasi intervensi spesifik (contoh: konseling, pengurangan SKS) berdasarkan profil risiko.
   + Feedback Loop: Mekanisme untuk dosen mencatat hasil intervensi, memperkaya data pelatihan model.
  
   Fitur early warning akan memicu kesadaran mandiri mahasiswa melalui pesan seperti, "Berdasarkan analisis, Anda berisiko DO karena IPK Semester 3 < 2.0. Disarankan konsultasi dengan dosen wali." Modul intervensi akan terintegrasi dengan kalender akademik, misalnya menyarankan pengurangan SKS untuk mahasiswa bekerja. Feedback loop dari dosen tentang efektivitas intervensi (misalnya, peningkatan IPK setelah konseling) akan digunakan untuk memperbaiki model.

 **Rencana pengembangan ini bertujuan menciptakan sistem prediksi DO yang lebih proaktif dan terintegrasi. Dengan kombinasi teknologi data mining, visualisasi, dan kolaborasi antar-departemen, universitas dapat mengurangi angka DO secara signifikan.**

# Conclusion 
Berdasarkan hasil analisis dan implementasi model prediksi risiko drop out mahasiswa menggunakan algoritma Decision Tree, dapat disimpulkan bahwa sistem yang dikembangkan telah mencapai tingkat akurasi yang sangat baik sebesar 94.25%. Model ini mampu mengidentifikasi mahasiswa berisiko drop out dengan precision 87% dan recall 65%, menunjukkan kemampuan yang seimbang antara ketepatan prediksi dan cakupan identifikasi kasus. Faktor-faktor seperti IPK semester awal, tingkat kehadiran, dan jumlah mata kuliah yang diulang terbukti menjadi penentu utama dalam prediksi risiko drop out. Implementasi sistem ini memberikan solusi efektif bagi universitas untuk melakukan intervensi akademik secara dini dan tepat sasaran, sekaligus mengoptimalkan alokasi sumber daya untuk program retensi mahasiswa. Keberhasilan model ini membuka peluang pengembangan lebih lanjut, termasuk integrasi dengan sistem akademik yang ada, penambahan variabel prediktor yang lebih komprehensif, serta pengembangan dashboard visual untuk memudahkan monitoring oleh pihak fakultas dan rektorat. Dengan demikian, sistem prediksi ini tidak hanya memberikan solusi teknis yang akurat tetapi juga menjadi alat strategis dalam meningkatkan kualitas pendidikan dan mengurangi angka drop out di tingkat perguruan tinggi.
  

 
   


