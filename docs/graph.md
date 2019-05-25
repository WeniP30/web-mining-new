graph digunakan untuk visualisasi struktur link dari website. kita akan menggambar graph dari edgelist yang telah kita buat sebelumnya.

```python
g = nx.from_pandas_edgelist(edgelistBox, "From", "To", None, nx.DiGraph())
pos = nx.spring_layout(g)

nx.draw(g, pos)
nx.draw_networkx_labels(g, pos, label, font_color="w")

plt.axis("off")
plt.show()
```

kita gunakan *Networkx* untuk membentuk graph berarah, kemudian kita visualisasikan menggunakan *Matplotlib*.

**Berikut graph yang terbentuk dari website "https://www.dicoding.com/"**

![Capture](img\Capture.PNG)

