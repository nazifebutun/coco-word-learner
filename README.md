# 📘 Image Classification & English → Turkish Translator  
**Akbank Derin Öğrenme Bootcamp – Final Project**  

---

## 🎯 Proje Amacı
Bu projenin amacı:  
- 📷 **Bir görselin içindeki nesneyi derin öğrenme modeli ile tanımak**  
- 🌍 **Tahmin edilen sınıfı hem İngilizce hem Türkçe göstermek**  
- 🎓 Öğrencileri **görsel tanıma + İngilizce öğrenmeye teşvik etmek**  

Proje, bilgisayarla görme (**Computer Vision**) ve doğal dil işleme (**NLP/Translation**) alanlarını bir araya getirerek özgün bir eğitim aracı ortaya koymaktadır.  

---

## 🗂 Kullanılan Veri Seti
- **COCO 2017 Dataset** (train2017, val2017)  
- Toplamda **80 sınıf** içeriyor:  
  `person, dog, car, laptop, soccer ball, tennis ball, cat...`  
- Bootcamp hız kısıtlarından dolayı bazı sınıf ve örneklerde örnekleme yapılmıştır.  

---

## 🛠 Kullanılan Teknolojiler
- **Python 3.11** (Kaggle Notebook ortamı)  
- **PyTorch** (ResNet50 transfer learning)  
- **Torchvision** (DataLoader, transforms)  
- **OpenCV** (görsel işleme)  
- **Matplotlib** (grafikler, görselleştirme)  
- **Deep Translator (Google Translate API)** (EN→TR çeviri)  

---

## 📑 Notebook Yapısı

### 🔹 A) Ortam Kurulumu
- GPU (CUDA) kontrolü yapıldı.  
- Gerekli kütüphaneler yüklendi.  

### 🔹 B) Veri Çerçevesi (COCO JSON → DataFrame)
- `instances_train2017.json` ve `instances_val2017.json` okundu.  
- Görsellerle eşleşen **class_id** ve **class_name** bilgileri DataFrame’e aktarıldı.  
- `KEEP_TOP_K` parametresi ile sınıf sayısı kısıtlanabiliyor.  

### 🔹 C) Sınıf Haritaları
- `name2id`, `id2name` sözlükleri oluşturuldu.  
- Modelin çıktısı kolayca sınıf ismine çevrilebiliyor.  

### 🔹 D) Dataset ve DataLoader
- **Data Augmentation**: `RandomResizedCrop`, `HorizontalFlip`, `ColorJitter`  
- Normalize: **ImageNet mean/std** değerleri  
- `CocoClsDataset` sınıfı ile görseller tensörlere dönüştürüldü.  
- `train_loader` ve `val_loader` oluşturuldu.  

### 🔹 E) Model Tanımı
- **ResNet50 (ImageNet pretrained)** kullanıldı.  
- Son katman (fc) → COCO sınıf sayısına göre güncellendi.  
- **Dropout** eklenerek overfitting azaltıldı.  

### 🔹 F) Eğitim ve Değerlendirme
- Loss: `CrossEntropyLoss`  
- Optimizer: `AdamW`  
- Scheduler: `StepLR`  
- `train_one_epoch` ve `evaluate` fonksiyonları ile eğitim döngüsü yazıldı.  
- **Accuracy & Loss grafikleri** çizildi.  

### 🔹 G) Çeviri Katmanı
- `translate_en_to_tr` fonksiyonu:  
  1. Mini sözlük (en sık geçen nesneler)  
  2. Cache  
  3. Google Translate API  
  4. Hata olursa İngilizce geri döndürme  
- Böylece modelin tahmin ettiği her sınıf etiketi hem **EN** hem **TR** çıktılandı.  

### 🔹 H) Tahmin + Görselleştirme
- Validation setinden rastgele bir görsel seçiliyor.  
- Top-5 tahmin üretiliyor:


Top-1: dog | TR: köpek | 93.5%
Top-2: cat | TR: kedi | 4.1%
Top-3: fox | TR: tilki | 1.2%


- Görsel üzerine overlay kutusu (EN + TR) yazılıyor.  
- Çıktılar hem notebook içinde gösteriliyor hem `output_overlay_trained/` klasörüne kaydediliyor.  

---

## 📊 Sonuçlar
- Eğitim doğruluğu: **%97**  
- Doğrulama doğruluğu: **%70** civarında  
- Görseller üzerinde nesne tanıma + Türkçe çeviri başarıyla çalıştı.  
<img width="609" height="397" alt="image" src="https://github.com/user-attachments/assets/fb04535a-4f70-4b6c-8582-3c52034676a3" />

<img width="633" height="437" alt="image" src="https://github.com/user-attachments/assets/9a8780f5-6aef-45df-95c3-1a3cfacbab13" />

<img width="650" height="394" alt="image" src="https://github.com/user-attachments/assets/5451bde7-7105-43b6-8658-2ea8d4a4c0ee" />

---

## 🌟 Özgün Katkı
Bu proje yalnızca bir görüntü sınıflandırma çalışması değil; aynı zamanda **İngilizce öğrenmeyi destekleyen etkileşimli bir araç**.  

- Model: nesneyi tanıyor  
- Sistem: İngilizce adını + Türkçe karşılığını gösteriyor  
- Kullanıcı: görseller üzerinden **görsel hafıza + dil öğrenimi** yapabiliyor  

---

## 📌 İleri Çalışmalar
- Daha güçlü model denemeleri (**EfficientNet, ViT**)  
- Hugging Face çeviri modelleriyle entegrasyon  
- Flask/Streamlit ile web arayüzü  
- Mobil uygulama versiyonu  

---

✨ **Sonuç:**  
Bu proje, bilgisayarla görme ve doğal dil işleme yöntemlerini birleştirerek hem teknik hem de eğitsel fayda sağlayan özgün bir çözüm ortaya koymuştur.  


