# Mercedes Atego — Simpack / Framer hazirligi

Kaynak: `source/mercedes+atego.obj` (Blender 2.93 ihraci, orijinal `.mtl` dosyasi kayipti).

## Konvansiyon
| | |
|---|---|
| Koordinat sistemi | ISO 8855 — **x ileri, y sol, z yukari** |
| Birim | metre (kaynak birimi **x 2.54** olceklendi) |
| Origin (govde dosyalari) | **on dingil merkezi, yol duzlemi** → x=0 on dingil ekseni, y=0 arac orta duzlemi, z=0 yol |
| Origin (tekerlekler) | her tekerlek **kendi merkezinde**, donme ekseni **y** |

## Olculer (dogrulanmis)
- Dingil mesafesi: **4.443 m**
- Lastik cap: **0.898 m** (merkez yuksekligi 0.449 m)
- Iz genisligi: on **2.035 m**, arka (cift lastik merkezleri) **1.901 m**
- Toplam: uzunluk **7.99 m**, genislik 2.69 m (aynalarla; kasa 2.44 m), yukseklik **3.355 m**
- On cikinti 1.31 m, arka cikinti 2.24 m

## Dosyalar

### `simpack/` — katı geometri (OBJ + tek ortak MTL)
| dosya | vertex | yuz | not |
|---|---|---|---|
| `atego_cab.obj` | 5736 | 4424 | kabin + on cam + aynalar + cati spoileri + on plaka |
| `atego_frame.obj` | 1342 | 1183 | sasi, traversler, yakit deposu |
| `atego_body.obj` | 2619 | 2581 | kasa + stop lambalari + arka plaka |
| `atego_detail.obj` | 1708 | 1734 | motor/suspansiyon detaylari (opsiyonel, gizlenebilir) |
| `atego_wheel_fl/fr.obj` | 2427 | 2749 | on tekerlek (tek lastik) |
| `atego_wheel_rl/rr.obj` | 4145 | 7756 | arka tekerlek (cift lastik) |
| `atego_full.obj` | 24549 | 30932 | hepsi tek parca, arac ekseninde |
| `atego.mtl` | | | duz renkli malzemeler, yeniden uretildi (doku yok) |
| `placements.csv` | | | tekerlek merkezlerinin arac eksenindeki konumu |

Tekerlek konumlari (arac ekseni, m):

    wheel_fl   0.000   +1.0174   0.4491
    wheel_fr   0.000   -1.0174   0.4491
    wheel_rl  -4.4428  +0.9505   0.4491
    wheel_rr  -4.4428  -0.9505   0.4491

### `simpack/wire/` ve `simpack/wire_fine/` — tel kafes
Dihedral aciya gore secilmis karakteristik kenarlar, OBJ `l` (line) elemani olarak.
- `wire/` : 60°, kisa kenarlar < 30 mm atildi → **5942 kenar** (sadece temel hatlar)
- `wire_fine/` : 35°, kisa kenarlar < 5 mm atildi → 16054 kenar (detayli)

Not: Simpack'in OBJ okuyucusu cizgi (`l`) elemanlarini cizmezse bu dosyalar bos gorunur;
o durumda kenarlarin ince seride/tupe donusturuldugu kati bir varyant uretilebilir.

### `web/atego.glb` — Framer / three.js
glTF konvansiyonuna cevrildi (**+Y yukari, -Z ileri**), parcalar ayri node:
`cab`, `frame`, `body`, `detail`, `wheel_fl/fr/rl/rr` — tekerlek node'lari kendi merkezlerinde,
yani dogrudan lokal eksende dondurulebilir. 1.25 MB.

### `preview/`
`atego_solid.png`, `atego_wire.png` (temel), `atego_wire_fine.png` (detayli) — yan/ust/on/izometrik kontrol goruntuleri.
`00_*.png` kaynak dosyanin ilk analizi.

## Kaynakta temizlenenler
- 3.74 x 3.74 m'lik zemin plane'i (`Plane.003_Plane.002`) silindi
- 32 nesne 8 mantikli parcaya toplandi
- Kayip `.mtl` malzeme adlarindan yeniden uretildi (`wire_RRGGBB` adlari gercek RGB degerlerini tasiyordu, onlar birebir kullanildi)
