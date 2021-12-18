### Custom-Logshipping dengan SQL Server

Proyek ini  bertujuan untuk membuat 
Proyek ini mengacu pada Logshipping yang telah dilakukan pada [halaman berikut](https://sqlperformance.com/2014/10/sql-performance/readable-secondaries-on-a-budget).

## Requirement

* 2 Instance SQL Server 2019

Satu instance digunakan sebagai database primary, dan satu instance sebagai secondary. Dalam proyek ini, primary instance bernama `SQLEXPRESS` dan secondary instance bernama `MSSQL`.

* Windows Task Scheduler

Task Scheduler digunakan untuk menjalankan script secara otomatis setiap waktu yang ditentukan.

* SQLCMD

SQLCMD merupakan aplikasi untuk menjalankan query SQL Server melalui Command Prompt

* PHP versi 8

Tested menggunakan PHP v8.0.13

* SQLSRV

SQLSRV merupakan penghubung dari PHP untuk dapat mengakses database di SQL Server. Instalasi dapat dilihat [di sini.](https://docs.microsoft.com/en-us/sql/connect/php/loading-the-php-sql-driver?view=sql-server-2017)

## Instalasi Logshipping

Instalasi aplikasi dilakukan dengan mengaktifkan koneksi kedua instance dan menjalankan file query secara berurutan yang ada pada folder 
/logshipping_query


#### 0. Create DB

Query ini akan membuat database dengan nama 
logshipped


#### 1. Add linked server

Membuat koneksi dengan server secondari yaitu ```MSSQL```.

#### 2. Create table

Membuat tabel pada database 
logshipped


Tabel yang dibuat yaitu:

* 
PMAG_Databases


Tabel ini akan digunakan untuk menyimpan nama database yang akan dibackup

* 
PMAG_Secondaries


Tabel ini akan digunakan untuk menyimpan informasi server secondary tempat akan dilakukan restore

* 
PMAG_LogBackupHistory


Tabel ini akan menyimpan riwayat backup yang telah dilakukan

* 
PMAG_LogRestoreHistory


Tabel ini akan menyimpan riwayat restore yang telah dilakukan

#### 3. PMAG_Backup SP

Membuat stored procedure yang akan dipanggil untuk melakukan backup dan restore. Stored procedure ini juga memanggil stored procedure 
PMAG_InitializeSecondaries
 dan 
PMAG_RestoreLogs
 ketika dijalankan.

#### 4. PMAG_InitializeSecondaries SP

Stored procedure ini menginisialisasi server secondary yang digunakan ketika backup dilakukan. Stored procedure ini juga memanggil stored procedure 
PMAG_Backup
 dan 
PMAG_RestoreLogs
 ketika dijalankan.

#### 5. PMAG_RestoreLogs SP

Stored procedure ini akan menjalankan proses restore setelah backup dilakukan.

#### 6. PMAG_CleanupHistory SP

Stored procedure ini akan digunakan untuk menghapus riwayat backup restore yang telah dilakukan.

#### 7. Insert table

Melakukan query insert ke table 
PMAG_Databases
 untuk mendefinisikan database yang akan dibackup dan restore, selain itu juga ke table 
PMAG_Secondaries
 untuk mendefinisikan server secondary yang akan digunakan.

#### 8. Full backup

Menjalankan stored procedure 
PMAG_Backup
 dengan type **bak** yaitu melakukan backup database secara keseluruhan

#### 9. Log backup

Menjalankan stored procedure 
PMAG_Backup
 dengan type **trn** yaitu melakukan backup berdasarkan kondisi/perubahan yang terjadi pada database
