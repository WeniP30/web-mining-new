Proses seleksi fitur digunakan untuk mengurangi jumlah kata/fitur yang tidak penting (sesuai hasil pembobotan), banyaknya fitur sangat berpengaruh pada hasil akhir clustering dan waktu untuk komputasi oleh karena itu seleksi fitur sangat dibutuhkan untuk melakukan penyusutan pada fitur yang akan digunakan.

**Pearson Correlation**

Merupakan metode seleksi fitur sederhana dengan cara mengukur korelasi/hubungan setiap fitur, semakin tinggi nilai korelasi maka semakin kuat hubungan fiturnya.

```python
def pearsonCalculate(data, u,v):
    "i, j is an index"
    atas=0; bawah_kiri=0; bawah_kanan = 0
    for k in range(len(data)):
        atas += (data[k,u] - meanFitur[u]) * (data[k,v] - meanFitur[v])
        bawah_kiri += (data[k,u] - meanFitur[u])**2
        bawah_kanan += (data[k,v] - meanFitur[v])**2
    bawah_kiri = bawah_kiri ** 0.5
    bawah_kanan = bawah_kanan ** 0.5
    return (atas/(bawah_kiri * bawah_kanan))
def meanF(data):
    meanFitur=[]
    for i in range(len(data[0])):
        meanFitur.append(sum(data[:,i])/len(data))
    return np.array(meanFitur)
def seleksiFiturPearson(data, threshold, berhasil):
    global meanFitur
    data = np.array(data)
    meanFitur = meanF(data)
    u=0
    while u < len(data[0]):
        dataBaru=data[:, :u+1]
        meanBaru=meanFitur[:u+1]
        seleksikata=berhasil[:u+1]
        v = u
        while v < len(data[0]):
            if u != v:
                value = pearsonCalculate(data, u,v)
                if value < threshold:
                    dataBaru = np.hstack((dataBaru, data[:, v].reshape(data.shape[0],1)))
                    meanBaru = np.hstack((meanBaru, meanFitur[v]))
                    seleksikata = np.hstack((seleksikata, berhasil[v]))
            v+=1
        data = dataBaru
        meanFitur=meanBaru
        berhasil=seleksikata
        if u%50 == 0 : print("proses : ", u, data.shape)
        u+=1
    return data, seleksikata

xBaru2,kataBaru = seleksiFiturPearson(tfidf, 0.9, berhasil)
xBaru1,kataBaru2 = seleksiFiturPearson(xBaru2, 0.8, berhasil)
```

