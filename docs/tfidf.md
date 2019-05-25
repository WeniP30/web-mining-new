TF-IDF  atau Term Frequence dan Invers Document Frequence adalah proses pembobotan term pada setiap data yang heterogen.

*<u>menghitung TF</u>*

TF sama dengan VSM yaitu menghitung frekuensi kemunculan kata pada setiap data.

```python
tf = matrix
```

*<u>menghitung IDF</u>*

menghitung jumlah data secara luas pada koleksi dokumen yang bersangkutan.

menghitung DF (Document Frekuensi)

**contoh :**

data 1 = "telur ayam goreng"

data 2 = "masak telur goreng makan ayam goreng"

| kata   | jumlah data yang mengandung kata tersebut |
| ------ | ----------------------------------------- |
| ayam   | 2                                         |
| goreng | 2                                         |
| masak  | 1                                         |
| makan  | 1                                         |
| telur  | 2                                         |

```python
df = list()
for d in range (len(matrix[0])):
    total = 0
    for i in range(len(matrix)):
        if matrix[i][d] !=0:
            total += 1
    df.append(total)

idf = list()
for i in df:
    tmp = 1 + log10(len(matrix)/(1+i))
    idf.append(tmp)
```

list *df* digunakan untuk menampung hasil perhitungan DF, kemudian kita hitung IDF yang merupakan hasil inverse dari DF dan kita tampung pada list *idf*.

```
tfidf = []
for baris in range(len(matrix)):
    tampungBaris = []
    for kolom in range(len(matrix[0])):
        tmp = tf[baris][kolom] * idf[kolom]
        tampungBaris.append(tmp)
    tfidf.append(tampungBaris)
```

Hitung TF-IDF, dengan mengalikan TF dengan IDF `tf-idf = tf x idf` , kemudian hasil tfidf disimpan pada list *tfidf*.

```python
with open('TFIDF.csv', mode='w') as employee_file:
    employee_writer = csv.writer(employee_file, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL)
    employee_writer.writerow(berhasil)
    for i in tfidf:
        employee_writer.writerow(i)
```

tampung hasil TF-IDF pada file csv.

> TF-IDF digunakan untuk mendapatkan bobot yang lebih akurat dibandingkan dengan hasil VSM.