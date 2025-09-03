# PUSULA_FERHAT_AKKOPRU
Ferhat Akköprü — akkopru_ferhat65@outlook.com

# Bulgular Özeti (EDA & Preprocessing)

## 1) Proje Özeti
- Amaç: Klinik veri üzerinde EDA ve modelleme öncesi veri hazırlığı.
- Çıktı: Temizlenmiş, kodlanmış, yeni özellikler eklenmiş veri; EDA görselleştirmeleri.

## 2) Veri Seti
- Kayıt: 2235
- Sütun türleri: Sayısal (ör. `Yas`), metin/kategorik (ör. `Cinsiyet`, `KanGrubu`), süre alanları (string -> int).

## 3) EDA Öne Çıkanlar
- Eksik değerler: `KanGrubu`, `Alerji`, `KronikHastalik`, `UygulamaYerleri` vb. değişkenlerde anlamlı boşluklar var.
- Tutarsızlıklar: “Polen” vs “POLEN” gibi büyük/küçük harf kaynaklı tekrarlar düzeltildi.
- Dağılımlar: Yaş ve süre değişkenleri pozitif, çoğunlukla sağa çarpık.
- Korelasyon: Süre sütunları arasında beklenen pozitif ilişkiler mevcut.

## 4) Preprocessing Adımları
- Eksik değer doldurma:
  - `TedaviAdi` bazlı mod doldurma: `UygulamaYerleri`, `Bolum`, `Tanilar`.
  - Kalan kategorikler: `unknown`.
- Metin normalizasyonu: `casefold`, fazla boşluk temizliği, çoklu etiket ayrıştırma.
- Kodlama:
  - İkili: `Male`, `Female`, `UlkeIci`, `Alerji_Var`, `Bolum_Fiziksel`.
  - Kan grubu: A/B/Rh/Unknown bayrakları.
  - Hiyerarşik gruplama ve one-hot/label encoding türevleri.
- Sayısal çıkarımlar:
  - `TedaviSuresi_int`, `UygulamaSuresi_int` (regex ile sayısal çekim).
  - `ToplamTedaviSuresi_dk = TedaviSuresi_int * UygulamaSuresi_int`.
- Yeni özellik:
  - `FizikselDegil_ve_Alerji` = (`Bolum_Fiziksel`==0) & (`Alerji_Var`==1).

## 5) Öneriler
- Booleans -> 0/1 dönüşümü (model ve scaler uyumu için).
- Outlier yönetimi (IQR) ve seçmeli ölçekleme (yalnızca sürekli sayısallar).
- Nadir kategorilerin grup/Other ile birleştirilmesi ve kalıcı OHE pipeline’ı.

## 6) Yeniden Üretim
- `README.md`’deki adımları izleyin, notebook’u baştan sona çalıştırın.
- hücre üstlerinden detaylı yorumlar ve yapılanlar yazılmıştır

## 7) Gereksinimler  
pandas>=2.0.0
numpy>=1.24.0
seaborn>=0.12.0
matplotlib>=3.7.0
scikit-learn>=1.3.0
openpyxl>=3.1.0
jupyterlab>=4.0.0
