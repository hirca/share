# Volvo FH16 + tenteli yari romork — Simpack / Framer hazirligi

Kaynak: `source/fh16.fbx` (3ds Max ihraci, FBX 7500) + `source/maps/` (21 doku dosyasi).
FBX dogrudan ayristirildi; 262 model dugumu, 259 geometri, 76 malzeme.
Bu dosyada parcalarin cogu (246 adet) **geometric transform** tasiyor, o da hesaba katildi.

## Konvansiyon
| | |
|---|---|
| Koordinat sistemi | ISO 8855 — **x ileri, y sol, z yukari** |
| Birim | metre (kaynak cm idi) |
| Origin (govde dosyalari) | **cekici on dingil merkezi, yol duzlemi** |
| Origin (tekerlekler) | her tekerlek **kendi lastik merkezinde**, donme ekseni **y** |

## Olculer (dogrulanmis)
- Toplam: uzunluk **18.61 m**, genislik **3.05 m** (aynalarla), yukseklik **4.19 m**
- Cekici dingil mesafesi: **3.929 m**
- Lastik cap: **1.080 m** (tum akslar)
- Iz genisligi: on **2.216 m**; ikiz lastikli akslarda lastik ciftinin merkezi ±0.924 m
- Romork dingilleri (x): **-11.195 / -12.587 / -13.979 m** → aks araligi 1.392 m

## Dosyalar

### `simpack/` — kati geometri (OBJ + ortak `fh16.mtl`)
Orijinal 3.05 M ucgen → **194 357 ucgen** (%6.4). Kaynaktaki lastik disleri asiri modellenmisti
(tek basina `Tyre1` malzemesi 1.3 M ucgen); butce yuzey alanina gore dagitildi.

| dosya | ucgen | origin (m) |
|---|---|---|
| `fh16_cab.obj` | 40 276 | 0,0,0 |
| `fh16_cab_interior.obj` | 10 571 | 0,0,0 — **ic mekan, disaridan gorunmez; istemezsen yukleme** |
| `fh16_tractor_chassis.obj` | 28 473 | 0,0,0 |
| `fh16_trailer.obj` | 34 847 | 0,0,0 |
| `fh16_wheel_fl / fr.obj` | ~8 000 | x 0.000, y ±1.108, z 0.540 |
| `fh16_wheel_rl / rr.obj` (ikiz) | ~8 150 | x -3.929, y ±0.924, z 0.540 |
| `fh16_trailer_wheel_1l…3r.obj` (ikiz) | ~8 000 | x -11.195 / -12.587 / -13.979, y ±0.924, z 0.540 |

Tam konum listesi: `simpack/placements.csv`.

### `simpack/wire/` ve `simpack/wire_fine/`
- `wire/` : govde 60°, tekerlek 30° → **33 728 kenar** (temel hatlar)
- `wire_fine/` : govde 35°, tekerlek 20° → 346 315 kenar

### `web/volvo_fh16.glb`
glTF konvansiyonu (+Y yukari, -Z ileri), 63 173 ucgen, 1.14 MB, parcalar ayri node.

### `source/maps/`
Modelin doku seti (21 dosya). **Not:** FBX'te Texture/Video dugumu yok — malzemeler doku
baglantisi tasimiyor, dolayisiyla UV eslemesi de aktarilmadi. Malzemeler FBX'teki difuz
renklerle duz renk olarak veriliyor (lastik koyu gri, deri kahve, Volvo mavi/kirmizi aksanlar).

## Parcalama nasil yapildi
Geometri 1 mm'de kaynaklanip 14 571 bagli bilesene ayrildi. Lastik imzasi (iki boyut esit,
cap 90-200 cm, ekseni yanal, merkez yuksekligi ≈ yaricap) ile 10 tekerlek gövdesi bulundu;
kalanlar boyuna konum + yukseklik ile kabin / cekici sasi / romork olarak ayrildi.
Ic mekan parcalari malzeme adindan (leather, fabric, interior, monitor, steering...) ayirt edildi.
