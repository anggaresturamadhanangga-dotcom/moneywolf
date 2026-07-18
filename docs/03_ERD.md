# 03. Entity Relationship Diagram (ERD)

## Tujuan

Dokumen ini menjelaskan struktur database MoneyWolf sebagai dasar pengembangan aplikasi.

---

# Tabel: users

## Fungsi

Menyimpan data akun pengguna.

| Field | Type | Keterangan |
|-------|------|------------|
| id | INT AUTO_INCREMENT | Primary Key |
| fullname | VARCHAR(100) | Nama lengkap |
| email | VARCHAR(100) | Email pengguna |
| password | VARCHAR(255) | Password (hashed) |
| created_at | TIMESTAMP | Tanggal dibuat |
| updated_at | TIMESTAMP | Terakhir diperbarui |

---

# Tabel: categories

## Fungsi

Menyimpan kategori transaksi.

| Field | Type | Keterangan |
|-------|------|------------|
| id | INT AUTO_INCREMENT | Primary Key |
| name | VARCHAR(100) | Nama kategori |
| type | ENUM('income','expense') | Jenis kategori |
| icon | VARCHAR(100) | Nama icon |
| color | VARCHAR(20) | Warna kategori |
| created_at | TIMESTAMP | Tanggal dibuat |

---

# Tabel: transactions

## Fungsi

Menyimpan seluruh transaksi pemasukan dan pengeluaran.

| Field | Type | Keterangan |
|-------|------|------------|
| id | INT AUTO_INCREMENT | Primary Key |
| user_id | INT | Foreign Key ke users |
| category_id | INT | Foreign Key ke categories |
| type | ENUM('income','expense') | Jenis transaksi |
| amount | DECIMAL(12,2) | Nominal transaksi |
| note | TEXT | Catatan transaksi |
| transaction_date | DATE | Tanggal transaksi |
| created_at | TIMESTAMP | Tanggal dibuat |
| updated_at | TIMESTAMP | Terakhir diperbarui |

---

# Tabel: budgets

## Fungsi

Menyimpan budget bulanan pengguna.

| Field | Type | Keterangan |
|-------|------|------------|
| id | INT AUTO_INCREMENT | Primary Key |
| user_id | INT | Foreign Key ke users |
| month | DATE | Bulan budget |
| amount | DECIMAL(12,2) | Total budget bulan tersebut |
| created_at | TIMESTAMP | Tanggal dibuat |
| updated_at | TIMESTAMP | Terakhir diperbarui |

---

# Tabel: installments

## Fungsi

Menyimpan data cicilan pengguna.

| Field | Type | Keterangan |
|-------|------|------------|
| id | INT AUTO_INCREMENT | Primary Key |
| user_id | INT | Foreign Key ke users |
| name | VARCHAR(100) | Nama cicilan |
| total_amount | DECIMAL(12,2) | Total cicilan |
| remaining | DECIMAL(12,2) | Sisa cicilan |
| monthly_payment | DECIMAL(12,2) | Cicilan per bulan |
| due_date | DATE | Tanggal jatuh tempo |
| status | ENUM('active','paid') | Status cicilan |
| created_at | TIMESTAMP | Tanggal dibuat |
| updated_at | TIMESTAMP | Terakhir diperbarui |

---

# Tabel: goals

## Fungsi

Menyimpan target keuangan pengguna.

| Field | Type | Keterangan |
|-------|------|------------|
| id | INT AUTO_INCREMENT | Primary Key |
| user_id | INT | Foreign Key ke users |
| title | VARCHAR(100) | Nama target |
| target_amount | DECIMAL(12,2) | Target dana |
| current_amount | DECIMAL(12,2) | Dana yang sudah terkumpul |
| target_date | DATE | Target selesai |
| status | ENUM('active','completed') | Status target |
| created_at | TIMESTAMP | Tanggal dibuat |
| updated_at | TIMESTAMP | Terakhir diperbarui |

---

# Relasi Database

users (1)
│
├──────< transactions (N)
│
├──────< budgets (N)
│
├──────< installments (N)
│
└──────< goals (N)

categories (1)
│
└──────< transactions (N)

---

# Catatan

- Satu user dapat memiliki banyak transaksi.
- Satu user dapat memiliki banyak budget (berbeda setiap bulan).
- Satu user dapat memiliki banyak cicilan.
- Satu user dapat memiliki banyak target keuangan.
- Satu kategori dapat digunakan oleh banyak transaksi.