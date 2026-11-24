# 🛒 E-Ticaret Satış Analizi ve SQLite Veri Entegrasyonu

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Veri%20Analizi-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Sentetik%20Veri-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Görselleştirme-11557C?style=for-the-badge)
![Seaborn](https://img.shields.io/badge/Seaborn-İstatistiksel%20Grafik-4C72B0?style=for-the-badge)
![SQLite](https://img.shields.io/badge/SQLite-Veritabanı-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

## 📌 Proje Özeti

Bu proje, sentetik olarak oluşturulan bir e-ticaret sipariş veri seti üzerinde uçtan uca **veri üretimi, keşifçi veri analizi (EDA), özellik mühendisliği (Feature Engineering), veri görselleştirme ve ilişkisel veritabanı (SQLite) sorgulama** süreçlerini kapsayan bir veri analitiği çalışmasıdır.

Proje kapsamında 300 adet e-ticaret siparişi Python ile üretilerek CSV formatında dışa aktarılmış, müşteri demografisi ve satış performansı çok boyutlu olarak incelenmiş, 5 farklı istatistiksel grafik tek bir panelde görselleştirilmiş ve işlenen veriler SQLite veritabanına aktarılarak SQL sorgularıyla doğrulanmıştır.

---

## 🎯 Proje Kapsamı ve İş Akışı

1. **Sentetik Veri Üretimi:** `NumPy` ve `Pandas` kullanılarak 300 satırlık sipariş verisi oluşturulur ve `ecommerce_sales.csv` dosyasına kaydedilir.
2. **Veri Keşfi ve Temel İstatistikler:** Veri tipleri, eksik değer durumu (`df.info()`), toplam sipariş, toplam satılan ürün adedi ve fiyat istatistikleri hesaplanır.
3. **Özellik Mühendisliği (Feature Engineering):**
   - `TotalPrice`: Birim fiyat ve sipariş adedi çarpılarak sipariş bazlı toplam tutar hesaplanır (`Price * Quantity`).
   - `AgeGroup`: Müşteri yaşları **Genç (18–25)**, **Yetişkin (26–40)**, **Orta Yaş (41–60)** ve **60+** segmentlerine ayrılır.
4. **Grup Bazlı Satış Analizleri:** Kategori gelirleri, ürün satış adetleri, şehir bazlı ciro, ödeme yöntemi tercihleri, yaş grubu harcamaları ve en yüksek tutarlı ilk 10 sipariş analiz edilir.
5. **Veri Görselleştirme:** `Matplotlib` ve `Seaborn` kullanılarak 5 grafikten oluşan kapsamlı bir görsel analiz paneli oluşturulur.
6. **SQLite Entegrasyonu:** İşlenen veri seti `ecommerce.db` veritabanındaki `orders` tablosuna aktarılır ve SQL sorguları ile kategori gelirleri ile İstanbul özelindeki en yüksek tutarlı siparişler raporlanır.

---

## 📊 Veri Seti Yapısı

Veri seti başlangıçta **8 ham sütun** ve **300 eksik değersiz (non-null)** kayıttan oluşur; özellik mühendisliği aşamasında **2 yeni sütun** eklenir:

| Sütun Adı | Veri Tipi | Açıklama |
| :--- | :--- | :--- |
| `OrderId` | `int64` | Benzersiz sipariş numarası (1 – 300) |
| `Product` | `str` | Ürün adı *(Laptop, Tişört, Roman, Parfüm, Tava, Kulaklık, Pantolon, Defter, Ruj, Lamba)* |
| `Category` | `str` | Ürün kategorisi *(Elektronik, Giyim, Kitap, Kozmetik, Ev)* |
| `Price` | `int32` | Ürün birim fiyatı (50 – 5.000 TL aralığında) |
| `Quantity` | `int32` | Sipariş edilen ürün adedi (1 – 5 adet) |
| `CustomerAge` | `int32` | Müşteri yaşı (18 – 69 yaş aralığında) |
| `City` | `str` | Siparişin verildiği şehir *(İstanbul, Ankara, İzmir, Bursa, Antalya)* |
| `PaymentType` | `str` | Ödeme yöntemi *(Kredi Kartı, Kapıda Ödeme, Havale/EFT)* |
| `TotalPrice` *(Türetilmiş)* | `int64` | Sipariş toplam tutarı (`Price * Quantity`) |
| `AgeGroup` *(Türetilmiş)* | `str` | Müşteri yaş segmenti *(Genç, Yetişkin, Orta Yaş, 60+)* |

---

## 📈 Öne Çıkan Analiz Bulguları

Notebook çalıştırıldığında üretilen mevcut veri seti üzerinden elde edilen temel metrikler aşağıdadır:

### Genel Satış Özeti
- **Toplam Sipariş Sayısı:** `300`
- **Toplam Satılan Ürün Adedi:** `908`
- **Toplam Ciro:** `2.442.812 TL`
- **Ortalama Ürün Birim Fiyatı:** `2.679,06 TL`
- **Fiyat Aralığı:** `101 TL` (Min) – `4.996 TL` (Max)
- **En Yüksek Tutarlı Tek Sipariş:** `24.925 TL` (`OrderId: 106`)

### Kırılım Bazlı Sonuçlar

| Analiz Boyutu | Lider Segment / Değer | Öne Çıkan Detay |
| :--- | :--- | :--- |
| **En Yüksek Gelirli Kategori** | **Ev** (`638.082 TL`) | İkinci sırada **Elektronik** (`534.188 TL`), en düşük gelirde **Kozmetik** (`350.926 TL`) |
| **En Çok Satılan Ürünler** | **Defter** ve **Ruj** (`109 adet`) | Üçüncü sırada **Kulaklık** (`107 adet`), en az satılan **Lamba** (`64 adet`) |
| **En Yüksek Satışlı Şehir** | **İstanbul** (`529.911 TL`) | İstanbul'u **Antalya** (`502.270 TL`) ve **Ankara** (`494.010 TL`) takip ediyor |
| **En Çok Tercih Edilen Ödeme** | **Kredi Kartı** (`111 sipariş` / `%37,0`) | **Kapıda Ödeme** (`95`) ve **Havale/EFT** (`94`) birbirine çok yakın dağılıyor |
| **En Yüksek Harcama Yapan Yaş Grubu** | **Orta Yaş (41–60)** (`1.026.685 TL`) | Toplam cironun `%42`sinden fazlasını oluşturuyor; ikinci sırada **Yetişkin** (`698.312 TL`) |

> **Not:** Veri seti rastgele sayı üretimi (`numpy.random`) ile oluşturulduğu için ilk hücre yeniden çalıştırıldığında sayısal değerler değişiklik gösterebilir.

---

## 🎨 Veri Görselleştirme

Proje içerisinde `sns.set_theme(style="whitegrid")` teması ve `3x2` subplot yerleşimi (`figsize=(16, 14)`) kullanılarak 5 farklı grafik üretilir:

1. **Kategorilere Göre Toplam Gelir** *(Bar Plot – `viridis` paleti)*
2. **Şehirlere Göre Toplam Satış** *(Bar Plot – `magma` paleti)*
3. **Ürün Fiyat Dağılımı** *(Histogram + KDE eğrisi – 20 bin)*
4. **Müşteri Yaşı ve Harcama İlişkisi** *(Scatter Plot)*
5. **Ödeme Yöntemlerine Göre Sipariş Sayısı** *(Count Plot – `Set2` paleti)*

<!-- Grafiği PNG olarak kaydedip repoya eklerseniz aşağıdaki satırı aktif edebilirsiniz: -->
<!-- ![E-Ticaret Analiz Paneli](images/dashboard.png) -->

---

## 🗄️ SQLite Veritabanı ve SQL Sorguları

Analiz edilen DataFrame, Python'un yerleşik `sqlite3` kütüphanesi aracılığıyla `ecommerce.db` veritabanındaki `orders` tablosuna aktarılır ve aşağıdaki SQL sorguları çalıştırılır:

```sql
-- 1. Kategorilere göre toplam gelir raporu
SELECT Category, SUM(TotalPrice) AS TotalRevenue
FROM orders
GROUP BY Category;

-- 2. İstanbul ilindeki en yüksek tutarlı ilk 5 sipariş
SELECT OrderId, Product, City, TotalPrice
FROM orders
WHERE City = 'İstanbul'
ORDER BY TotalPrice DESC
LIMIT 5;
```

**İstanbul En Yüksek Sipariş Çıktısı (Örnek):** `OrderId: 124` — Laptop (`23.765 TL`)

---

## 📁 Proje Dosya Yapısı

```text
├── ecommerce_analysis.ipynb   # Ana analiz, görselleştirme ve SQLite notebook dosyası
├── ecommerce_sales.csv        # Üretilen sentetik e-ticaret veri seti
├── ecommerce.db               # Python üzerinden oluşturulan SQLite veritabanı
└── README.md                  # Proje dokümantasyonu
```

---

## ⚙️ Kurulum ve Çalıştırma

Projeyi yerel ortamınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz:

### 1. Repoyu Klonlayın
```bash
git clone https://github.com/esmanuryavuz908/e-ticaret-satis-analizi-python-sql.git
cd e-ticaret-satis-analizi-python-sql
```

### 2. Gerekli Kütüphaneleri Yükleyin
```bash
pip install pandas numpy matplotlib seaborn jupyter
```
*(Not: `sqlite3` Python standart kütüphanesinde yerleşik olarak gelir, ek kurulum gerektirmez.)*

### 3. Notebook'u Başlatın
```bash
jupyter notebook
```
Açılan arayüzden `.ipynb` dosyasını seçip hücreleri sırayla çalıştırabilirsiniz.

---

## 🚀 Geliştirilebilir Alanlar

- **Tekrarlanabilirlik (Reproducibility):** Sentetik veri üretim aşamasına `np.random.seed(42)` eklenerek her çalıştırmada tutarlı sonuçlar elde edilebilir.
- **Gerçekçi Ürün-Kategori Eşleştirmesi:** Ürünlerin rastgele kategoriler yerine kendi gerçek kategorileriyle eşleşeceği bir sözlük (dictionary) yapısı kurulabilir.
- **Zaman Serisi Analizi:** Sipariş tarihi (`OrderDate`) sütunu eklenerek aylık/mevsimsel satış trendleri incelenebilir.
- **Seaborn Güncellemesi:** `barplot` ve `countplot` fonksiyonlarında `hue` parametresi tanımlanarak gelecek sürüm uyarıları (`FutureWarning`) giderilebilir.

---

## 👩‍💻 Geliştirici

**Esmanur Yavuz**  
Veri Bilimi ve Analitiği Öğrencisi
