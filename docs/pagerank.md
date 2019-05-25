page rank merupakan nilai yang digunakan untuk mengukur link populer dari suatu website. page rank ditentukan oleh banyaknya link yang menuju ke website tersebut. biasanya digunakan untuk menentukan rangking sebuah website dalam mesin pencari.

untuk menghitung page rank kita gunakan code berikut :

```python
damping = 0.85
max_loop = 100
error_toleransi = 0.0001
pr = nx.pagerank(g, alpha = damping, max_iter=max_loop, tol=error_toleransi)
```

> secara default damping factor bernilai 0.85

```python
nodelist = g.nodes
label= {}
data = []
for i, key in enumerate(nodelist):
    data.append((pr[key], key))
    label[key]=i
```

page rank yang sudah kita hitung ditampung dalam list data, dengan key adalah node (link) dari website yang di crawl.

kemudian urutkan page rank dari yang terbesar ke yang terkecil untuk menemukan page rank yang paling tinggi. page rank yang paling tinggi berarti node (link) sering diakses oleh node lainnya.

```python
urut = data.copy()
for x in range(len(urut)):
    for y in range(len(urut)):
        if urut[x][0] > urut[y][0]:
            urut[x],urut[y] = urut[y],urut[x]
        
urut = pd.DataFrame(urut, None, ("PageRank", "Node"))
print(urut)
```

**Berikut hasil 10 page rank teratas dari "https://www.dicoding.com/"**

| No   | Page rank | Node                             |
| ---- | --------- | -------------------------------- |
| 0    | 0.022732  | http://google.com/               |
| 1    | 0.020266  | https://accounts.google.com/     |
| 2    | 0.014959  | https://twitter.com/             |
| 3    | 0.013869  | https://developers.google.com/   |
| 4    | 0.013718  | http://facebook.com/             |
| 5    | 0.012229  | http://youtube.com/              |
| 6    | 0.011484  | https://l.facebook.com/          |
| 7    | 0.011484  | https://developers.facebook.com/ |
| 8    | 0.010891  | https://blog.dicoding.com/       |
| 9    | 0.010891  | http://dicoding.com/             |

