Clustering dilakukan untuk mengelompokkan  data dengan karakteristik yang sama ke suatu ‘class’ yang sama dan data dengan karakteristik yang berbeda ke ‘class’ yang lain.

Pada permasalahan ini digunakan fuzzy c-means, untuk mengelopokkan data menjadi 3 class. 

```python
cntr, u, u0, distant, fObj, iterasi, fpc =  fuzz.cmeans(xBaru1.T, 3, 2, 0.00001, 1000, seed=0)
membership = np.argmax(u, axis=0)
```

`fuzz.cmeans(xBaru1.T, 3, 2, 0.00001, 1000, seed=0)`

parameter dari fuzzy c-means : data, jumlah cluster, pembobot, eror maksimal dan iterasi maksimal.

Menghitung *Silhouette* untuk mengetahui jarak kedekatan atau realasi fitur dalam tiap cluster

```python
silhouette = silhouette_samples(xBaru1, membership)
s_avg = silhouette_score(xBaru1, membership, random_state=10)
```

*<u>Simpan hasil clustering ke file csv</u>*

```python
def write_csv(nama_file, isi, tipe='w'):
    'tipe=w; write; tipe=a; append;'
    with open(nama_file, mode=tipe) as tbl:
        tbl_writer = csv.writer(tbl, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL)
        for row in isi:
            tbl_writer.writerow(row)
write_csv("Cluster.csv", [["Cluster"]])
write_csv("Cluster.csv", [membership],        "a")
write_csv("Cluster.csv", [["silhouette"]],    "a")
write_csv("Cluster.csv", [silhouette],        "a")
write_csv("Cluster.csv", [["Keanggotaan"]],   "a")
write_csv("Cluster.csv", u,                   "a")
write_csv("Cluster.csv", [["pusat Cluster"]], "a")
write_csv("Cluster.csv", cntr,                "a")
```

