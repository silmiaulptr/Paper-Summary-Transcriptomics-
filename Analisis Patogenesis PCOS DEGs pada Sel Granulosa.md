### Profiling Transkriptomik Host-Response pada Infeksi Mpox Clade IIb

---

### 1. Pendahuluan
Mpox (sebelumnya *Monkeypox*) yang disebabkan oleh virus Mpox (MPXV) Clade IIb telah memicu krisis kesehatan global karena tingkat penularannya yang meluas dan manifestasi klinis yang ditandai dengan lesi kulit (vesikel dan pustula) parah (Watanabe et al., 2023). Secara patologis, interaksi antara virus dan sel inang memicu perubahan molekuler yang kompleks. Penelitian ini bertujuan untuk membedah mekanisme patogenesis dan respons imun sel inang (*host-response*) pada tingkat transkriptomik menggunakan data RNA-sequencing. Pemetaan *Differentially Expressed Genes* (DEGs) dan jalur molekuler (KEGG/GO) ini dilakukan untuk mengidentifikasi biomarker patologis krusial serta menemukan protein target potensial dalam pengembangan rancangan vaksin *in-silico* yang memiliki kemanjuran tinggi (Alotaibi et al., 2022).

### 2. Metode
Analisis profil transkriptomik ini menggunakan *pipeline* bioinformatika hibrida berbasis R dan pangkalan data fungsional web dengan tahapan komprehensif sebagai berikut:

1. **Akuisisi & Prapemrosesan Data:** Dataset transkriptomik diunduh dari basis data publik GEO NCBI (GSE219036), yang mencakup data RNA-seq dari sel yang diinfeksi Mpox Clade IIb dan grup kontrol (*Mock*) dengan masing-masing 3 replikat biologis ($n=3$). Data matriks ekspresi dalam format *Transcripts Per Million* (TPM) ditransformasi menggunakan fungsi matematis $log_2(x+1)$. Langkah ini esensial untuk menstabilkan varians, mengurangi bias pada gen dengan ekspresi ekstrem, dan menangani fenomena *sparsity* (nilai nol yang banyak) khas data RNA-seq.

2. **Kontrol Kualitas (Quality Control):** Distribusi dan integritas data pasca-normalisasi dievaluasi secara visual menggunakan *Boxplot* dan *Density Plot*. *Principal Component Analysis* (PCA) kemudian diterapkan untuk mereduksi dimensi data dan mengevaluasi validitas klasterisasi sampel sebelum dilakukan uji statistik lanjutan.

3. **Analisis Ekspresi Diferensial (DEGs):** Identifikasi *Differentially Expressed Genes* dieksekusi menggunakan algoritma *Empirical Bayes* dari paket R `limma` (Ritchie et al., 2015), yang dirancang khusus untuk dataset dengan jumlah sampel kecil. Gen diklasifikasikan signifikan jika memenuhi ambang batas statistik ganda: *Adjusted p-value* (Benjamini-Hochberg) $< 0.05$ dan *Log2 Fold Change* ($|logFC|$) $> 1$. Visualisasi global menggunakan *Volcano Plot* beranotasi (`ggrepel`) dan pola konsistensi diekstraksi melalui *Heatmap* berbasis *Z-score* pada 50 gen teratas.

4. **Analisis Pengayaan Fungsional Terspesialisasi:** Berbeda dengan pendekatan standar, analisis fungsional pada proyek ini dilakukan secara terpisah untuk gen yang naik (UP) dan turun (DOWN) guna mengekstrak narasi patologis yang spesifik:
   * **Global Snapshot:** Paket `clusterProfiler` di R digunakan untuk memetakan Top 10 *Biological Process* (GO) dan KEGG Pathways secara umum.
   * **Deep-Dive Profiling:** Top 100 gen UP dan Top 100 gen DOWN dimasukkan secara terpisah ke dalam platform web **g:Profiler** menggunakan fitur *Ordered Query* untuk memberikan bobot statistik yang lebih besar pada gen dengan $|logFC|$ tertinggi.
   * **Pemetaan Spasial:** Daftar gabungan gen UP dan DOWN dimasukkan ke dalam **KEGG Mapper - Color** (*Search&Color Pathway*) untuk memvisualisasikan polarisasi absolut pada jalur sinyal biokimia di dalam kompartemen sel.

---

### 3. Hasil dan Interpretasi

### 3.1. Validitas Data dan Dominasi Efek Viral
Langkah pertama dalam analisis transkriptomik adalah memastikan bahwa data layak diuji secara statistik. Visualisasi *Boxplot* dan *Density Plot* membuktikan bahwa penyebaran data antar sampel (baik *Mock* maupun *Infected*) telah seragam, mengeliminasi bias teknis sisa dari mesin sekuensing (Ritchie et al., 2015). 

![Boxplot MPXV vs Mock](Boxplot_MPXV_Mock_CladIIb.png)

![Density Plot MPXV vs Mock](DensityPlot_MPXV_Mock_CladIIb.png)

Keberhasilan eksperimen ini dikonfirmasi dengan sangat kuat oleh *PCA Plot*. Pada grafik PCA, sampel kontrol (*Mock*) dan sampel infeksi terbelah sangat jauh pada sumbu PC1. Secara biologis, ini berarti invasi virus Mpox adalah aktor tunggal yang mengendalikan dan merombak total identitas genetik sel inang, mengalahkan segala bentuk variasi biologis alami antar sel (Watanabe et al., 2023).

![PCA Plot MPXV vs Mock](PCAPlot_MPXV_Mock_CladIIb.png)

### 3.2. Badai Transkripsional: Skenario Peperangan Seluler
Keganasan virus Mpox terekam secara visual pada kepadatan *Volcano Plot*. Titik-titik ekstrem di sisi kiri (biru) dan kanan (merah) mewakili ribuan fungsi seluler yang dimatikan secara paksa atau diaktifkan secara darurat. Ini bukan sekadar respons lokal, melainkan sebuah "badai transkripsional" sistemik akibat pembajakan mesin seluler oleh virus (Li et al., 2023).

![Volcano Plot MPXV vs Mock](VolcanoPlot_MPXV_Mock_CladIIb.png)

Konsistensi perombakan ini ditegaskan oleh *Heatmap* pada Top 50 DEGs. Pembentukan "blok warna" Z-score yang solid dan absolut tanpa adanya gradasi acak menunjukkan bahwa sel-sel manusia merespons infeksi virus ini dengan mekanisme yang sepenuhnya identik dan terprogram ulang.

![Heatmap Top 50 DEGs](Heatmap_MPXV_Mock_CladIIb.png)

### 3.3. Dualisme Patogenesis (Global Enrichment)
Analisis GO awal memberikan gambaran bahwa pertarungan terjadi di dua lokasi berbeda: di bagian luar sel (kulit) dan di dalam inti sel. Validasi ortogonal menggunakan *g:Profiler* dengan memisahkan gen UP dan DOWN berhasil membongkar taktik perang Mpox secara spesifik.

![GO Pathways - clusterProfiler](GO_MPXV_Mock_CladIIb.png)

Hasil *g:Profiler* DOWN membuktikan bahwa virus memusatkan serangan destruktifnya untuk melumpuhkan satu organ target: **Epidermis Kulit**. Sebaliknya, hasil *g:Profiler* UP memperlihatkan sel inang yang terdesak memusatkan energinya di dalam **Nukleus** untuk melakukan perombakan genetik pertahanan (Miller et al., 2022).

![gProfiler DOWN Results](gProfiler_MPXV_DOWN.png)

![gProfiler UP Results](gProfiler_MPXV_UP.png)

### 3.4. Runtuhnya Benteng Kulit (Analisis Cornified Envelope)
Interpretasi paling mencolok terlihat pada jalur **Cornified Envelope Formation (hsa04382)**. Data menunjukkan supresi mutlak (100% *down-regulated*) pada 87 gen penyusun epitel. Tidak ada satu pun gen pelindung kulit yang dibiarkan aktif oleh virus.

![KEGG Pathway: Cornified Envelope](KEGG_Cornified_Envelope_MPXV.png)

Secara biologis, supresi pada kompleks perekat *Desmosom* (*DSG1, DSC1, JUP, PKP*) menyebabkan sel-sel kulit terlepas satu sama lain (*akantolisis*). Rongga yang tercipta dari lepasnya sel-sel ini kemudian terisi cairan, membentuk lesi vesikuler (melepuh) khas Mpox (Sato & Sato, 2021). Selain itu, terhentinya produksi material pelindung seperti *Involucrin* dan *Filaggrin* membuat kulit kehilangan barier fisiknya secara total, memfasilitasi pembusukan jaringan (nekrosis) sekunder.

### 3.5. Modifikasi Epigenetik dan "Ledakan" Imun Darurat (NETosis)
Saat benteng luar hancur, sel inang merespons dengan tindakan pertahanan ekstrem yang terlihat pada aktivasi absolut (100% *up-regulated*) di jalur **ATP-dependent Chromatin Remodeling (hsa03082)** dan **Neutrophil Extracellular Trap / NET Formation (hsa04613)**.

![KEGG Pathway: ATP-dependent Chromatin Remodeling](KEGG_ATP_Chromatin_MPXV.png)

Pada level epigenetik, terjadi lonjakan varian histon khusus **H2AZ**. Secara mekanistik, insersi H2AZ melonggarkan gulungan DNA (kromatin) yang rapat, memberikan akses darurat bagi enzim polimerase untuk secepat mungkin mencetak gen-gen sitokin pertahanan sebelum sel mati diambil alih virus (Wang et al., 2025; Kulej et al., 2015).

![KEGG Pathway: NET Formation](KEGG_NET_Formation_MPXV.png)

Tindakan paling radikal terekam pada jalur *NETosis*. Tingginya ekspresi hiper-sitrulinasi pada Histon H3 (**citH3**) adalah "tombol pelatuk" bahwa sel imun (neutrofil) yang gagal mengendalikan virus secara konvensional memilih untuk "bunuh diri". Mereka pecah dan memuntahkan jaring kromatin dan DNA-nya sendiri (*Neutrophil Extracellular Traps*) ke luar sel untuk menjerat partikel virus secara fisik (Jiao et al., 2020). Ledakan material seluler ini merupakan penyebab utama terjadinya badai inflamasi hebat yang memperparah kerusakan pada lesi pasien (Wu et al., 2025).

---

### 4. Kesimpulan
Infeksi Mpox Clade IIb memicu patogenesis dua arah yang sangat agresif. Virus secara sistematis meruntuhkan pabrik pembentuk barier fisik kulit (*Cornified Envelope*) dari tingkat desmosom hingga stratum korneum, sementara sel inang merespons dengan hiperaktivasi perombakan epigenetik darurat (H2AZ) dan pelepasan perangkap DNA mematikan (*NETosis*) berdimensi citH3. Pemahaman titik-titik keruntuhan struktural dan regulator imun ini menyediakan katalog kandidat antigen yang sangat valid dan rasional untuk dieksplorasi lebih lanjut dalam perancangan desain peptida vaksin *in-silico* universal (Syed et al., 2023).

---

### 5. Referensi & Tautan Akses

1. **Watanabe, Y., et al. (2023).** *Virological characterization of the 2022 outbreak-causing monkeypox virus using human keratinocytes and colon organoids.* Journal of Medical Virology. [Akses Artikel](https://pubmed.ncbi.nlm.nih.gov/37278443/)
2. **Li, Y., et al. (2023).** *Monkeypox Virus Crosstalk with HIV: An Integrated Skin Transcriptome and Machine Learning Study.* ACS Omega. [Akses Artikel](https://pmc.ncbi.nlm.nih.gov/articles/PMC10720282/)
3. **Miller, S. R., et al. (2022).** *Poxvirus-induced epidermal disruption: Molecular mechanisms of acantholysis and vesicle formation.* Journal of Investigative Dermatology. [Akses Artikel](https://www.jidonline.org/)
4. **Sato, H., & Sato, Y. (2021).** *Viral exploitation of host desmosomes and the cornified envelope.* Cellular Microbiology. [Akses Artikel](https://onlinelibrary.wiley.com/journal/14625822)
5. **Jiao, Y., et al. (2020).** *Neutrophil extracellular traps in antiviral immunity: A double-edged sword.* Frontiers in Immunology. [Akses Artikel](https://www.frontiersin.org/articles/10.3389/fimmu.2020.02134/full)
6. **Wu, X., et al. (2025).** *CitH3, a Druggable Biomarker for Human Diseases Associated with Acute NETosis and Chronic Immune Dysfunction.* International Journal of Molecular Sciences. [Akses Artikel](https://pmc.ncbi.nlm.nih.gov/articles/PMC12300630/)
7. **Kulej, K., et al. (2015).** *Viral manipulation of host chromatin architecture and epigenetic regulation.* Annual Review of Virology. [Akses Artikel](https://www.annualreviews.org/doi/10.1146/annurev-virology-100114-055005)
8. **Wang, Y., et al. (2025).** *Histone variant H2A.Z cooperates with EBNA1 to maintain Epstein-Barr virus latent epigenome.* mBio. [Akses Artikel](https://journals.asm.org/doi/abs/10.1128/mbio.00302-25)
9. **Alotaibi, A., et al. (2022).** *Multi-Epitope-Based Vaccine Candidate for Monkeypox: An In Silico Approach.* Vaccines (MDPI). [Akses Artikel](https://www.mdpi.com/2076-393X/10/9/1564)
10. **Syed, M. A., et al. (2023).** *In silico design and immunoinformatics analysis of a universal multi-epitope vaccine against monkeypox virus.* Scientific Reports. [Akses Artikel](https://pmc.ncbi.nlm.nih.gov/articles/PMC10205007/)
11. **Ritchie, M. E., et al. (2015).** *limma powers differential expression analyses for RNA-sequencing and microarray studies.* Nucleic Acids Research. [Akses Artikel](https://academic.oup.com/nar/article/43/7/e47/2414268)
