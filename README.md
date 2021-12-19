### Custom-Logshipping dengan SQL ServerCancel changes

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
