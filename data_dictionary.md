# 📖 Data Dictionary: Proyek Cocokin (Final Architecture)

Dokumen ini memuat definisi dan deskripsi dari seluruh variabel yang digunakan dalam *pipeline* data platform **Cocokin**, yang terbagi ke dalam 4 (empat) dataset terpisah.

---

## 1. Data Profil Kandidat (`cocokin_candidate_data.csv`)
Dataset yang berisi informasi rekam jejak, kualifikasi, dan keahlian dari pelamar kerja (kandidat) hasil pembersihan awal.

| Nama Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `candidate_id` | `String` | ID unik untuk mengidentifikasi setiap kandidat secara spesifik. |
| `industry_sector` | `String` | Sektor industri utama tempat kandidat berkarir atau melamar. |
| `candidate_skills` | `List (String)` | Daftar teks yang berisi seluruh keahlian (*skills*) yang diklaim dimiliki oleh kandidat pada portofolionya. |
| `experience_years` | `Integer` | Total akumulasi tahun pengalaman kerja aktual yang dimiliki kandidat. |
| `education_level` | `String` | Tingkat pendidikan tertinggi yang diselesaikan oleh kandidat (Misal: *Bachelor's, Master's*). |
| `skill_count` | `Integer` | Jumlah total keahlian yang dimiliki kandidat. |

---

## 2. Data Lowongan Pekerjaan / Industri (`cocokin_industry_data.csv`)
Dataset bersumber dari data *job postings* LinkedIn historis yang mewakili kebutuhan spesifik pasar kerja.

| Nama Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `job_id` | `String` | ID unik untuk mengidentifikasi lowongan pekerjaan. |
| `industry_sector` | `String` | Sektor industri dari perusahaan yang membuka lowongan tersebut. |
| `job_title` | `String` | Nama posisi atau jabatan pekerjaan yang ditawarkan. |
| `required_skills` | `List (String)` | Daftar keahlian wajib (*mandatory skills*) yang diminta perusahaan. |
| `minimum_experience_years` | `Integer` | Syarat batas minimum tahun pengalaman kerja yang diminta. |
| `education_level` | `String` | Syarat tingkat pendidikan minimum yang diminta. |
| `market_demand_score` | `Float` | Skor (1-10) yang menunjukkan tingkat seberapa dicari posisi ini di pasar kerja. |
| `location` | `String` | Lokasi geografis penempatan pekerjaan. |
| `formatted_work_type` | `String` | Kategori tipe pekerjaan (Contoh: *Full-time, Part-time*). |
| `formatted_experience_level` | `String` | Kategori level senioritas (Contoh: *Entry level, Mid-Senior level*). |
| `avg_salary` | `Float` | Rata-rata kompensasi finansial (**USD per Bulan / Monthly USD**). |
| `is_salary_confidential` | `Boolean` | Penanda (`1` atau `0`) apakah informasi gaji dirahasiakan oleh perusahaan. |
| `remote_allowed` | `Float/Boolean` | Penanda (`1.0` atau `NaN`) apakah pekerjaan mengizinkan sistem kerja jarak jauh. |

---

## 3. Master Dataset Rekayasa (`cocokin_engineered.csv`)
Dataset ini adalah **induk data (Master Data)** hasil penggabungan profil kandidat dan lowongan. Data ini dipertahankan secara utuh untuk keperluan Analisis Internal (BI/Data Analyst), Visualisasi *Dashboard*, dan logika *Explainability* (menampilkan kelemahan kandidat) di *Backend*.

| Nama Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `candidate_id` | `String` | Identitas unik kandidat. |
| `industry_sector_cand` | `String` | Sektor industri asli dari profil kandidat. |
| `candidate_skills` | `List` | Daftar keahlian awal milik kandidat. |
| `experience_years` | `Integer` | Tahun pengalaman aktual kandidat. |
| `education_level_cand` | `String` | Tingkat pendidikan aktual kandidat. |
| `skill_count` | `Integer` | Jumlah skill kandidat. |
| `sector_key` | `String` | Sektor industri yang telah distandarisasi kapital. |
| `job_id` | `String` | Identitas unik lowongan pekerjaan. |
| `industry_sector_job` | `String` | Sektor industri asli dari lowongan. |
| `job_title` | `String` | Judul pekerjaan yang ditawarkan. |
| `required_skills` | `List` | Daftar keahlian yang diwajibkan pekerjaan. |
| `minimum_experience_years` | `Integer` | Syarat minimum pengalaman kerja. |
| `education_level_job` | `String` | Syarat tingkat pendidikan lowongan. |
| `market_demand_score` | `Float` | Skor permintaan pasar (1-10). |
| `location` | `String` | Lokasi pekerjaan. |
| `formatted_work_type` | `String` | Tipe kontrak pekerjaan. |
| `formatted_experience_level` | `String` | Tingkat senioritas pekerjaan. |
| `avg_salary` | `Float` | Gaji rata-rata dalam USD per bulan. |
| `is_salary_confidential` | `Boolean` | Penanda kerahasiaan gaji. |
| `remote_allowed` | `Float` | Penanda dukungan kerja jarak jauh. |
| `cand_soft_skills` | `List` | Ekstraksi *soft skills* kandidat. |
| `cand_tech_skills` | `List` | Ekstraksi *tech/hard skills* kandidat. |
| `req_soft_skills` | `List` | Ekstraksi *soft skills* yang diminta lowongan. |
| `req_tech_skills` | `List` | Ekstraksi *tech/hard skills* yang diminta lowongan. |
| `skill_match_ratio` | `Float` | Rasio kecocokan keahlian berbobot (TF-IDF). |
| `missing_skills` | `List` | Daftar skill yang diminta tetapi tidak dimiliki kandidat. |
| `missing_skill_count` | `Integer` | Jumlah skill yang kurang (*missing*). |
| `experience_gap_years` | `Integer` | Selisih tahun pengalaman (0 = memenuhi syarat). |
| `edu_gap` | `Integer` | Selisih tingkat pendidikan ordinal (0 = memenuhi syarat). |
| `salary_percentile` | `Float` | Daya saing gaji relatif terhadap sektor industrinya (0-1). |
| `demand_n` | `Float` | Skor tingkat permintaan yang dinormalisasi (0-1). |
| `overall_fit_score` | `Float` | Skor kecocokan komposit mentah. |
| `scaled_fit_score` | `Float` | Skor kecocokan komposit akhir yang dinormalisasi (0-1). |

---

## 4. AI Training Dataset (`cocokin_training_ai.csv`)
Dataset ini dioptimalkan khusus untuk **Pelatihan Machine Learning (AI)**. Seluruh kolom hasil kalkulasi matematis (seperti `skill_match_ratio` dan `experience_gap`) tidak digunakan untuk mencegah *Data Leakage*. AI diwajibkan memprediksi skor berdasarkan data mentah dan pembacaan teks melalui NLP (*Natural Language Processing*).

| Nama Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `candidate_id` | `String` | Metadata yang wajib di-drop saat training. |
| `industry_sector_cand` | `String` | Metadata yang wajib di-drop saat training. |
| `candidate_skills` | `List` | Metadata yang wajib di-drop saat training. |
| `experience_years` | `Integer` | **Fitur Numerik:** Total pengalaman awal kandidat. |
| `education_level_cand` | `String` | **Fitur Kategorikal:** Pendidikan kandidat (Wajib di-Encode, misal: *OrdinalEncoder*). |
| `skill_count` | `Integer` | Metadata yang wajib di-drop saat training. |
| `sector_key` | `String` | **Fitur Kategorikal:** Sektor industri (Wajib di-Encode, misal: *OneHotEncoder*). |
| `job_id` | `String` | Metadata yang wajib di-drop saat training. |
| `industry_sector_job` | `String` | Metadata yang wajib di-drop saat training. |
| `job_title` | `String` | Metadata yang wajib di-drop saat training. |
| `required_skills` | `List` | Metadata yang wajib di-drop saat training. |
| `minimum_experience_years` | `Integer` | **Fitur Numerik:** Pengalaman minimum lowongan. |
| `education_level_job` | `String` | **Fitur Kategorikal:** Pendidikan minimum lowongan (Wajib di-Encode). |
| `market_demand_score` | `Float` | Metadata yang wajib di-drop saat training. |
| `location` | `String` | Metadata yang wajib di-drop saat training. |
| `formatted_work_type` | `String` | Metadata yang wajib di-drop saat training. |
| `formatted_experience_level` | `String` | Metadata yang wajib di-drop saat training. |
| `avg_salary` | `Float` | Metadata yang wajib di-drop saat training. |
| `is_salary_confidential` | `Boolean` | Metadata yang wajib di-drop saat training. |
| `remote_allowed` | `Float` | Metadata yang wajib di-drop saat training. |
| `cand_soft_skills` | `List` | **Fitur NLP:** Teks *soft skills* kandidat (Diproses dengan TF-IDF / Vectorizer). |
| `cand_tech_skills` | `List` | **Fitur NLP Utama:** Teks *hard skills* kandidat (Diproses dengan TF-IDF / Vectorizer). |
| `req_soft_skills` | `List` | **Fitur NLP:** Teks *soft skills* lowongan (Diproses dengan TF-IDF / Vectorizer). |
| `req_tech_skills` | `List` | **Fitur NLP Utama:** Teks *hard skills* lowongan (Diproses dengan TF-IDF / Vectorizer). |
| `skill_match_ratio` | `Float` | **Leakage (Drop):** Dihapus karena memberikan "bocoran" jawaban ke AI. |
| `missing_skills` | `List` | Metadata yang wajib di-drop saat training. |
| `missing_skill_count` | `Integer` | **Leakage (Drop):** Dihapus karena memberikan "bocoran" kelemahan kandidat ke AI. |
| `experience_gap_years` | `Integer` | **Leakage (Drop):** Dihapus agar AI menghitung sendiri jarak pengalaman dari fitur numerik. |
| `edu_gap` | `Integer` | **Leakage (Drop):** Dihapus agar AI mempelajari pola hierarki pendidikan secara mandiri. |
| `salary_percentile` | `Float` | **Leakage (Drop):** Dihapus (Kecuali jika dimasukkan ke dalam model sentimen gaji yang terpisah). |
| `demand_n` | `Float` | **Leakage (Drop):** Dihapus karena merupakan variabel buatan. |
| `overall_fit_score` | `Float` | **Leakage (Drop):** Wajib di-drop karena merupakan sumber perhitungan target. |
| `scaled_fit_score` | `Float` | **Target Label (Y):** Probabilitas kecocokan komposit akhir yang akan ditebak oleh AI (Skala 0.0 - 1.0). |