VSM merupakan proses menghitung frekuensi kemunculan setiap kata pada setiap data, dalam bentuk matriks.

**contoh :**

- data 1 = "telur ayam goreng"
- data 2 = "masak telur goreng makan ayam goreng"

| data ke | ayam | goreng | masak | makan | telur |
| ------- | ---- | ------ | ----- | ----- | ----- |
| 1       | 1    | 1      | 0     | 0     | 1     |
| 2       | 1    | 2      | 1     | 1     | 1     |

```python
conn = sqlite3.connect('events.db')
matrix=[]
cursor = conn.execute("SELECT* from EVENTS")
for row in cursor:
    tampung = []
    for i in berhasil:
        tampung.append(row[2].lower().count(i))
    matrix.append(tampung)
```

code diatas akan mengecek dan menghitung berapa kali kata pada list *berhasil*  muncul pada setiap baris data dalam tabel EVENTS di database *events.db*, kemudian menampung hasil frekuensi kemunculan `.count() ` dalam list *matrix*.

```python
with open('VSMkbi.csv', mode='w') as employee_file:
    employee_writer = csv.writer(employee_file, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL)
    employee_writer.writerow(berhasil)
    for i in matrix:
        employee_writer.writerow(i)
```

kemudian simpan hasil dalam file csv, dengan kolom pertama berisi kata/fitur dan kolom selanjutnya berisi matrix frekuensi kemunculan.