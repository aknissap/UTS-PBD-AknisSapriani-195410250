# UTS-PBD-AknisSapriani-195410250
NO 1<br>
3 DBMS yang bisa digunakan untuk mengelola big data<br>
 a. RDBMS = IBM DB2, MySQL, Microsoft SQL Server, dan Microsoft Access.<br>
 b. ORDBMS= Oracle Database , PostgreSQL , dan Microsoft SQL Server .<br>
 c. OODBMS= Database berorientasi objek Versant , Objectivity / DB , ObjectDB , dan ObjectStore .<br>
NO 2 <br>
Carilah contoh masalah big data yang bisa dikelola menggunakan salah satu DBMS tersebut, jelaskan mulai dari instalasi sampai CRUD untuk data menggunakan DBMS tersebut. Asumsikan anda akan memecahkan masalah big data yang sudah anda cari contoh tadi, 
jelaskan kira-kira bagaimana arsitektur dari solusi big data menggunakan DBMS tersebut, gambarkan diagramnya.
<br>
Membuat Halaman CRUD Python dan MySQL dengan menggunakan ubuntu kasus toko mainan
1. Instalasi Modul MySQL Connector
   Ketik peritah berikut untuk menginstal modul mysql untuk Python.<br>
   $ sudo apt install python3-mysql.connector ATAU pip3 install mysql-connector
2. Koneksi ke MySQL dan membuat connect.py<br>
import mysql.connector<br>
db = mysql.connector.connect(<br>
  host="localhost",<br>
  user="admin",<br>
  passwd="admin"<br>
)<br>
if db.is_connected()<br>
  print("Berhasil terhubung ke database")<br>
3. Jalankan connect.py dengan Python 3.<br>
   $python3 connect.py<br>
   Ketika berhasil akan ada keterangan berhasil terhubung Ke Database<br>
4. Kita membutuhkan modul mysql.connector untuk membuat koneksi ke MySQL.<br>
   $import mysql.connector<br>
    Lalu kita membuat koneksi dengan memanggil fungsi connect() dan parameter host, user, dan passwd.<br>
db = mysql.connector.connect(<br>
  host="localhost",
  user="admin",
  passwd="admin"
)<br>
5. Jika menggunakan XAMPP, menggunakan parameter seperti dibawah:<br>
db = mysql.connector.connect(<br>
  host="localhost",
  user="root",
  passwd="")<br>
6. Karena user default di XAMPP adalah root dan di sana biasanya tidak menggunakan password lalu cek koneksi.<br>
if db.is_connected():
  print("Berhasil terhubung ke database")<br>
7. Membuat Database
Membuat objek cursor kita tinggal buat seperti dibawah:<br>
cursor = db.cursor()<br>
8. Lalu untuk mengeksekusi query, tinggal panggil method execute() dengan parameter string query.<br>
cursor.execute(sql)<br>
9. Membuat file baru bernama create_db.py. Kemudian isi dengan kode berikut:<br>
import mysql.connector<br>
db = mysql.connector.connect(<br>
  host="localhost",<br>
  user="admin",<br>
  passwd="admin"<br>
)<br>
cursor = db.cursor()<br>
cursor.execute("CREATE DATABASE toko_mainan")<br>
print("Database berhasil dibuat!")<br>
![](PBD/1.PNG)<br>
10. Setelah itu menjalankan create_db.py dengan Python 3.<br>
python3 create_db.py<br>
Maka akan ada keterangan database dibuat<br>
11. Membuat database toko mainan<br>
db = mysql.connector.connect(<br>
  host="localhost",<br>
  user="admin",<br>
  passwd="admin",<br>
  database="toko_mainan"<br>
)<br>
12. Membuat file baru bernama create_table.py<br>
import mysql.connector
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="toko_mainan"
)
<br>
cursor = db.cursor()
sql = """CREATE TABLE customers (
  customer_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  address Varchar(255)
)
"""
cursor.execute(sql)
print("Tabel customers berhasil dibuat!")
<br>
13. Akan ada keterangan tabel customor telah dibuat
python3 create_table.py
![](PBD/2.PNG)<br>
14. Membuat file baru bernama insert_one.py kemudian isi dengan kode berikut:<br>
import mysql.connector
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="toko_mainan"
)
<br>
cursor = db.cursor()
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("Dian", "Mataram")
cursor.execute(sql, val)
<br>
db.commit()
<br>
print("{} data ditambahkan".format(cursor.rowcount))<br>
15. Kode untuk insert data <br>
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("Dian", "Mataram")
cursor.execute(sql, val)<br>
db.commit()<br>
16. Menampilkan data dengan membuat file baru bernama select.py kemudia isi dengan kode berikut:<br>
import mysql.connector
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="toko_mainan"
)<br>

cursor = db.cursor()
sql = "SELECT * FROM customers"
cursor.execute(sql)
<br>
results = cursor.fetchall()
<br>
for data in results:
  print(data)<br>
17. Update Data dengan membuat file baru bernama update.py. Kemudian isi dengan kode berikut:
import mysql.connector<br>
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="toko_mainan"
)<br>
cursor = db.cursor()
sql = "UPDATE customers SET name=%s, address=%s WHERE customer_id=%s"
val = ("Ardianta", "Lombok", 1)
cursor.execute(sql, val)
<br>
db.commit()
<br>
print("{} data diubah".format(cursor.rowcount))<br>
18. Menghapus Data dengan membuat file baru bernama delete.py, kemudian isi dengan kode berikut:<br>
import mysql.connector
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="toko_mainan"
)
<br>
cursor = db.cursor()
sql = "DELETE FROM customers WHERE customer_id=%s"
val = (1, )
cursor.execute(sql, val)
<br>
db.commit()
<br>
print("{} data dihapus".format(cursor.rowcount))<br>
19 . Aplikasi CRUDS berbasis CLI dengan membuat file baru bernama app_cruds.py, kemudian isi dengan kode berikut:<br>
import mysql.connector
import os
<br>
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="toko_mainan"
)<br>
def insert_data(db):
  name = input("Masukan nama: ")
  address = input("Masukan alamat: ")
  val = (name, address)
  cursor = db.cursor()
  sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
  cursor.execute(sql, val)
  db.commit()
  print("{} data berhasil disimpan".format(cursor.rowcount))<br>
def show_data(db):
  cursor = db.cursor()
  sql = "SELECT * FROM customers"
  cursor.execute(sql)
  results = cursor.fetchall()<br>
  if cursor.rowcount < 0:
    print("Tidak ada data")<br>
  else:
    for data in results:
      print(data)<br>
def update_data(db):<br>
  cursor = db.cursor()
  show_data(db)
  customer_id = input("pilih id customer> ")
  name = input("Nama baru: ")
  address = input("Alamat baru: ")
  sql = "UPDATE customers SET name=%s, address=%s WHERE customer_id=%s"
  val = (name, address, customer_id)
  cursor.execute(sql, val)<br>
  db.commit()<br>
  print("{} data berhasil diubah".format(cursor.rowcount))<br>
def delete_data(db):
  cursor = db.cursor()
  show_data(db)
  customer_id = input("pilih id customer> ")
  sql = "DELETE FROM customers WHERE customer_id=%s"
  val = (customer_id,)
  cursor.execute(sql, val)
  db.commit()
  print("{} data berhasil dihapus".format(cursor.rowcount))<br>
def search_data(db):
  cursor = db.cursor()
  keyword = input("Kata kunci: ")
  sql = "SELECT * FROM customers WHERE name LIKE %s OR address LIKE %s"
  val = ("%{}%".format(keyword), "%{}%".format(keyword))
  cursor.execute(sql, val)
  results = cursor.fetchall()<br>
  if cursor.rowcount < 0:
    print("Tidak ada data")<br>
  else:
    for data in results:
      print(data)<br>
def show_menu(db):<br>
  print("=== APLIKASI DATABASE PYTHON ===")<br>
  print("1. Insert Data")<br>
  print("2. Tampilkan Data")<br>
  print("3. Update Data")<br>
  print("4. Hapus Data")<br>
  print("5. Cari Data")<br>
  print("0. Keluar")<br>
  print("------------------")<br>
  menu = input("Pilih menu> ")
  #clear screen
  os.system("clear")
<br>
  if menu == "1":
    insert_data(db)
  elif menu == "2":
    show_data(db)
  elif menu == "3":
    update_data(db)
  elif menu == "4":
    delete_data(db)
  elif menu == "5":
    search_data(db)
  elif menu == "0":
    exit()
  else:
    print("Menu salah!")
if __name__ == "__main__":
<br>
  while(True):
    show_menu(db)
