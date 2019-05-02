Pada tahap ini, data yang telah kita dapat perlu dilakukan pre-processing atau seleksi untuk mendapatkan *key word* yang akan menjadi sebuah fitur (kata penting).

Tahapan preprocessing :

1. Tokenisasi, proses pemecahan kata menjadi index-index tersendiri
2. Stopword, proses seleksi membuang kata yang termasuk kata hubung dan tanda baca
3. Stemming, proses pengambilan kata dasar dari setiap kata
4. Seleksi berdasarkan KBI, kata dasar yang telah didapat dari porses *stemming* akan dicocokan pada kata yang terdapat pada database KBI untuk mendapatkan kata baku saja.

Menambahkan kosa kata tidak penting pada list *stopword* dengan cara manual, yaitu mengakses `Sastrawi\StopWordRemover\StopWordRemoverFactory.py` dari library python anda `Anaconda3\Lib\site-packages\`.

<u>*ekstraksi kata dasar :*</u> 

```python
factory = StopWordRemoverFactory()
stopword = factory.create_stop_word_remover ()
factorym = StemmerFactory ()
stemmer = factorym.create_stemmer ()

tmp = ''
for i in deskripsi:
    tmp = tmp + ' ' +i

hasil = []
for i in tmp.split():
    try :
        if i.isalpha() and (not i in hasil) and len(i)>2:
            # Menghilangkan Kata tidak penting
            stop = stopword.remove(i)
            if stop != "":
                out = stemmer.stem(stop)
                hasil.append(out)
    except:
        continue
katadasar=hasil
```

Code diatas digunakan untuk mengekstaksi kata dasar, membuang fitur yang bukan berupa text dan fitur yang termasuk kata hubung menggunakan library dari sastrawi.

**contoh :**

> - input : "saya jalan2 membeli sayur di pasar"
> - output : "saya" "jalan" "beli" "sayur" "pasar"

------

<u>*cek kata dalam KBI :*</u>

```python
conn = sqlite3.connect('KBI.db')
cur_kbi = conn.execute("SELECT* from KATA")
def LinearSearch (kbi,kata):
    found=False
    posisi=0
    while posisi < len (kata) and not found :
        if kata[posisi]==kbi:
            found=True
        posisi=posisi+1
    return found
```

Dalam proses ini kita memerlukan database KBI untuk mengecek setiap kata yang sesuai/baku. Kemudian buat sebuah function *LinearSearch* untuk mengecek setiap kata pada *katadasar* yang sesuai dengan KBI, dengan return value *found* . 

> found bernilai true - false

```python
berhasil=[]
for kata in cur_kbi :
    ketemu=LinearSearch(kata[0],katadasar)
    if ketemu :
        kata = kata[0]
        berhasil.append(kata)
```

- Jika *found=true* maka kata tersebut merupakan kata baku sesuai KBI, jadi kata tersebut kita simpan pada list *berhasil*. 
- Jika *found=false* maka kata tersebut bukan kata baku sesuai KBI, jadi kata tersebut tidak perlu disimpan.