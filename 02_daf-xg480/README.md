# 2021 DAF XG 480 + Cold Store Trailer — Simpack / Framer hazirligi

Kaynak: `source/2021+DAF+XG+480+Cold+Store+Trailer.fbx` (Cinema 4D ihraci, FBX 7500).
Ayni modelin 306 MB'lik OBJ ihraci silindi: normalleri yoktu, `.mtl`'i ve dokulari eksikti.
FBX dogrudan ayristirildi (Blender kullanilmadi); geometri, malzeme renkleri ve 16 gomulu doku cikarildi.

## Konvansiyon
| | |
|---|---|
| Koordinat sistemi | ISO 8855 — **x ileri, y sol, z yukari** |
| Birim | metre (kaynak cm idi) |
| Origin (govde dosyalari) | **cekici on dingil merkezi, yol duzlemi** |
| Origin (tekerlekler) | her tekerlek **kendi lastik merkezinde**, donme ekseni **y** |

## Olculer (dogrulanmis)
- Toplam: uzunluk **19.30 m**, genislik **3.07 m** (aynalarla; kasa 2.55 m), yukseklik **4.40 m**
- Cekici dingil mesafesi: **4.072 m**
- Lastik cap: on/cekici **1.093 m**, dorse **1.124 m**
- Iz genisligi: on **2.253 m**; cekici arka ikiz lastik merkezleri ±0.969 m
- Dorse dingilleri (x): **-11.428 / -12.773 / -14.111 m** → aks araligi 1.344 / 1.339 m
- Parca sinirlari (x): kabin +1.608..-2.041 | cekici sasi +1.598..-5.118 | dorse -1.951..-17.695

## Dosyalar

### `simpack/` — kati geometri (OBJ + ortak `daf.mtl`)
Orijinal 3.79 M ucgen → **227 267 ucgen** (%6) sadelestirildi. Butce alan bazli dagitildi:
buyuk yuzeyler cok, bijon/perckin gibi ufak parcalar az pay aldi; 2.5 cm'den kucuk 347 bilesen atildi.

| dosya | ucgen | origin (m) |
|---|---|---|
| `daf_cab.obj` | 57 666 | 0,0,0 |
| `daf_tractor_chassis.obj` | 33 104 | 0,0,0 |
| `daf_trailer.obj` | 40 558 | 0,0,0 |
| `daf_wheel_fl / fr.obj` | ~9 400 | x 0.000, y ±1.126, z 0.547 |
| `daf_wheel_rl / rr.obj` (ikiz) | ~9 000 | x -4.072, y ±0.970, z 0.547 |
| `daf_trailer_wheel_1l…3r.obj` | ~9 850 | x -11.428 / -12.762 / -14.104, y ±1.13, z 0.562 |

Tam konum listesi: `simpack/placements.csv`.

### `simpack/wire/` ve `simpack/wire_fine/` — tel kafes (OBJ `l` elemani)
- `wire/` : govde 60°, tekerlek 30°, min kenar 12/4 cm → **41 509 kenar** (temel hatlar)
- `wire_fine/` : govde 35°, tekerlek 20°, min kenar 5/2 cm → 169 158 kenar

### `simpack/tex/` — FBX'in icinden cikan 16 doku (9.2 MB)
Car Paint, Paint 1/2, Pneu (lastik), Light 1-4, 03/06/07.jpg.
**Not:** OBJ'lere UV yazilmadi; malzemeler FBX'teki difuz renklerle (12 farkli renk) duz renk olarak veriliyor.
Dokulu surum gerekiyorsa UV aktarimi ayrica yapilir.

### `web/daf_xg480.glb` — Framer / three.js
glTF konvansiyonu (+Y yukari, -Z ileri), 62 108 ucgen, 1.2 MB. Parcalar ayri node;
tekerlek node'lari kendi merkezlerinde, dogrudan dondurulebilir. Kaynak parcalar `web/parts/`.

### `preview/`
`daf_solid.png`, `daf_wire.png`, `daf_wire_fine.png` — yan/ust/on/izometrik kontrol goruntuleri.

## Parcalama nasil yapildi
FBX'teki 198 mesh ve 114 malzeme adi anlamsizdi (`Cold_Store_Trailer_N`, `Paint_N`), bu yuzden
geometri kaynaklanip (1 mm) bagli bilesenlere ayrildi (21 796 bilesen) ve kural bazli gruplandi:
lastik imzasi (iki boyutu esit, cap 95-160 cm, ekseni yanal) ile 10 tekerlek; kalanlar
boyuna konum + yukseklik esigi ile kabin / cekici sasi / dorse olarak ayrildi.
