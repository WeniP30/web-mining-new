Lakukan import untuk requirement :

```python
from requests import get
from bs4 import BeautifulSoup
import sqlite3
import csv
from Sastrawi.Stemmer.StemmerFactory import StemmerFactory
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory
from math import log10
import numpy as np
from sklearn.metrics import silhouette_samples, silhouette_score
import skfuzzy as fuzz
```

Proses pertama adalah melakukan scan/crawl pada halaman web, dan mengambil data yang diinginkan.

*<u>Proses crawl :</u>*

```python
judul=[]
developer=[]
deskripsi=[]
urls=[str(i) for i in range (1,11)]
```

Buat list untuk menampung masing-masing data yang kita inginkan, yaitu data judul, developer dan deskripsi dari 10 halaman. List *urls* digunakan untuk menampung page/halaman yang diinginkan, dengan range dari page ke-1 sampai page ke-10.

> pada program kita set range 1-11 karena stop looping dari program adalah n-1

```python
for url in urls :
    page=get("https://www.dicoding.com/events?q=&criteria=&sort=&sort_direction=desc&page="+url)
```

Lakukan get pada alamat website yang akan dicrawl, dapat dilihat pada bagian belakang alamat website terdapat variable *url*. url menampung informasi nomor halaman yang akan dicrawl.

**contoh :**

> urls = 1 sampai 10
>
> kita mulai dari, url = 1
>
> page=get("https://www.dicoding.com/events?q=&criteria=&sort=&sort_direction=desc&page="+"1")
>
> link : https://www.dicoding.com/events?q=&criteria=&sort=&sort_direction=desc&page=1
>
> maka akan mengakses page ke-1 dari website
>
> Iterasi akan terus berjalan sampai url=10

```python
	soup=BeautifulSoup(page.content,'html.parser')
    jdl=soup.findAll(class_='item-box-name')
    dev=soup.findAll('div',attrs={'class':'item-box-main-information'})
    desk=soup.findAll('div',attrs={'class':'item-box-main-information'})
```

`soup.findAll()` digunakan untuk mencari dan mengambil data berdasarkan class pada tag html dari website. Untuk mendapatkan class tag html perlu dilakukan *inspeksi elemen.*

> cara melakukan inspeksi elemen :
>
> block informasi yang dicari - klik kanan - inspeksi elemen - cari class yang menampung informasi
>
> - data judul : `<a class='item-box-name'>`
> - data developer : `<div class='item-box-main-information'>`
> - data deskripsi : `<div class='item-box-main-information'>`

```python
	for a in range (len(jdl)):
        judul+=[jdl[a].getText()]
    for b in range (len(dev)):
        developer+=[dev[b].find('p').text]
    for c in range(len(desk)):
        deskripsi+=[desk[c].find_all('p')[1].text]
```

`.getText()` dan `.text` digunakan untuk mengubah data menjadi text yang kemudian disimpan pada list yang sudah dibuat sebelumnya.

------

*<u>Save data ke db :</u>*

Setelah berhasil mengambil data dari setiap halaman, kita tampung dalam db menggunakan sqlite.

```python
conn = sqlite3.connect('events.db')
conn.execute('''CREATE TABLE if not exists EVENTS
         (NAMA_EVENT VARCHAR NOT NULL,
         DEVELOPER VARCHAR NOT NULL,
         DESKRIPSI VARCHAR NOT NULL);''')
for i in range (len(judul)):
    conn.execute('INSERT INTO EVENTS(NAMA_EVENT,DEVELOPER,DESKRIPSI) values (?, ?, ?)', (judul[i], developer[i], deskripsi[i]))
```

Code diatas digunakan untuk membuat db *events*, dengan nama tabel *EVENTS* dan 3 kolom yaitu NAMA_EVENT , DEVELOPER dan DESKRIPSI. 

Kemudian insert setiap data yang terdapat pada list *judul , developer dan deskripsi* ke setiap kolom pada tabel.