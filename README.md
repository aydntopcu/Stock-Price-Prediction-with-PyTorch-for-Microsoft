# Stock Price Prediction with PyTorch — LSTM vs GRU (DJIA 30 Stock Time Series)

Bu proje, Microsoft AI Summer School programı kapsamında geliştirilmiştir. Kaggle DJIA 30 Stock Time Series veri seti kullanılarak tekil hisse senedi (varsayılan: **AAPL**) fiyat tahmini üzerine gerçekleştirilen bir zaman serisi regresyon çalışmasıdır.

Saf zaman serisi mimarilerinin performansına odaklanır özellikle PyTorch ile implement edilen **LSTM (Long Short-Term Memory)** ve **GRU (Gated Recurrent Unit)** modellerini karşılaştırır.

---

## 📂 Proje Yapısı

```text
Stock_Price_Prediction/
├── stock price predicton with pytorch.ipynb    # Kodları, grafikleri ve analizleri içeren ana Notebook
├── data/
│   ├── AAPL_2006-01-01_to_2018-01-01.csv       # Tarihsel Apple hisse senedi veri seti
│   ├── all_stocks_2006-01-01_to_2018-01-01.csv # Tüm DJIA 30 veri seti (2006-2018)
│   ├── all_stocks_2017-01-01_to_2018-01-01.csv # Tüm DJIA 30 veri seti (2017-2018)
│   └── results_summary.csv                     # Kaydedilen model performans metrikleri
└── README.md                                   # Proje dokümantasyonu
```

---

## ⚙️ Gereksinimler

```bash
pip install torch pandas numpy scikit-learn matplotlib
```

## ▶️ Çalıştırma

1. Bu depoyu klonlayın veya indirin.
2. `stock price predicton with pytorch.ipynb` dosyasını Jupyter Notebook / JupyterLab ile açın.
3. **Kernel → Restart & Run All** ile baştan sona çalıştırın. Notebook, `data/` klasöründeki AAPL dosyasını otomatik bulup yükler; farklı bir hisseyle çalışmak isterseniz notebook içindeki `STOCK_SYMBOL` değişkenini değiştirmeniz yeterlidir.

## 📊 Sonuçlar

Veri: AAPL, 2006-01-03 → 2017-12-29 (3019 gün). Split tarihi: 2015-08-10 (train: 2415, test: 604 gün).

| Model | MSE     | RMSE   | Eğitim Süresi (s) |
|-------|---------|--------|-------------------|
| LSTM  | 80.6767 | 8.9820 | ~6.4              |
| GRU   | 34.5609 | 5.8788 | ~7.2              |

**Bulgular:**
- **GRU, LSTM'e kıyasla RMSE'de yaklaşık %34 daha düşük hata sergiledi** bu veri seti ve hiperparametreler için daha sağlam bir mimari.
- Test setinin ilk yarısında (fiyat yatay seyrederken) her iki model de gerçek fiyatı başarıyla takip ediyor. Asıl ayrışma, hissenin hızla yükseldiği son ~200 günde ortaya çıkıyor. LSTM bu ivmeyi yakalayamayıp düzleşirken, GRU nispeten daha iyi takip ediyor; ancak ikisi de klasik RNN "lag" (geriden gelme) zaafından tam olarak kaçamıyor.
- Eğitim süresi teorik beklentinin (GRU'nun daha az parametreyle daha hızlı eğitilmesi) tersine çıktı — bu, mimarinin kendisinden değil, kullanılan ortamdaki CPU/thread davranışından kaynaklanıyor.

## ⚠️ Sınırlamalar

- Model yalnızca geçmiş fiyat hareketlerine dayanıyor; makroekonomik göstergeler, şirket bilançoları, haber akışı veya piyasa duyarlılığı (sentiment) gibi dış faktörleri içermiyor.
- Tek bir train/test split ve sabit seed kullanıldı; bulguların tutarlılığını doğrulamak için walk-forward validation önerilir.
- Elde edilen hata metrikleri, modelin gerçek yatırım kararları için tek başına yeterli olmadığını gösteriyor ("AI Snake Oil" perspektifiyle tutarlı bir bulgu).

## 🔭 Sonraki Adımlar

- `LOOKBACK` pencere boyutu ve `HIDDEN_SIZE` hiperparametrelerinin optimize edilmesi
- Aşırı öğrenmeyi (overfitting) azaltmak için Dropout katmanlarının entegre edilmesi
- Çalışmanın farklı DJIA bileşenleriyle (örn. Microsoft, Boeing) tekrarlanarak bulguların genellenebilirliğinin test edilmesi
