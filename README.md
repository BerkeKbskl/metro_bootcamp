# Sürücüsüz Metro Simülasyonu - Rota Optimizasyonu

## 1. Proje Başlığı ve Kısa Açıklama
**Metro Ağı Rota Optimizasyon Sistemi**  
Bu proje, bir metro ağında iki istasyon arasındaki en hızlı ve en az aktarmalı rotaları bulan bir simülasyon sistemidir. Graf veri yapısı kullanılarak modelleme yapılmış, BFS ve A* algoritmaları ile optimizasyon sağlanmıştır.

---

## 2. Kullanılan Teknolojiler ve Kütüphaneler
- **Python 3.12**: Temel programlama dili
- `collections.deque`: BFS algoritmasında kuyruk yönetimi için
- `heapq`: A* algoritmasında öncelik kuyruğu oluşturmak için
- `defaultdict`: Hat bazlı istasyon gruplama için
- **OOP (Nesne Yönelimli Programlama)**: Kod organizasyonu için

---

## 3. Algoritmaların Çalışma Mantığı

### BFS Algoritması (En Az Aktarma)
- **Nasıl Çalışır?**  
  - İstasyonları katman katman dolaşır.
  - Her adımda hat değişim sayısını takip eder.
  - İlk bulduğu geçerli rotayı döndürür (BFS'in en kısa yol garantisi).
- **Neden Kullanıldı?**  
  Aktarma sayısını "graf derinliği" olarak ele aldığı için optimal çözüm verir.

### A* Algoritması (En Hızlı Rota)
- **Nasıl Çalışır?**  
  - Mevcut süre + tahmini kalan süre (heuristic) ile öncelik belirler.
  - Zaman maliyetini sürekli güncelleyerek ilerler.
- **Neden Kullanıldı?**  
  Tren süreleri farklı olduğundan, ağırlıklı graf yapısında en verimli algoritmadır.

---

## 4. Örnek Kullanım ve Test Sonuçları

### Temel Kullanım
```python
# Metro ağı oluşturma
metro = MetroAgi()
metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
metro.baglanti_ekle("K1", "M2", 2)  # Aktarma bağlantısı

# Rota sorgulama
rota = metro.en_az_aktarma_bul("M1", "K4")
hizli_rota = metro.en_hizli_rota_bul("T4", "M1")
```

### Test Sonuçları

| Test No | Başlangıç İstasyonu | Bitiş İstasyonu | En Az Aktarmalı Rota                                    | En Hızlı Rota (Dakika) |
|---------|----------------------|------------------|---------------------------------------------------------|------------------------|
| 1       | AŞTİ                  | OSB              | AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB           | 25 dakika             |
| 2       | Batıkent              | Keçiören         | Batıkent -> Demetevler -> Gar -> Keçiören              | 21 dakika             |
| 3       | Keçiören              | AŞTİ              | Keçiören -> Gar -> Gar -> Sıhhiye -> Kızılay -> AŞTİ           | 19 dakika             |
---

## 5. Projeyi Geliştirme Fikirleri
- **Gerçek Veri Entegrasyonu**  
  Ankara Metro verilerinin CSV/JSON formatında yüklenmesi.

- **Görsel Arayüz**  
  Tkinter ile interaktif metro haritası.

- **API Entegrasyonu**  
  Flask/Django ile web servisi oluşturma.

- **Gerçek Zamanlı Takip**  
  Kullanıcı konumuna göre dinamik rota güncelleme.

- **Performans Optimizasyonu**  
  Büyük veri setleri için Dijkstra + A* hibrit algoritma.
