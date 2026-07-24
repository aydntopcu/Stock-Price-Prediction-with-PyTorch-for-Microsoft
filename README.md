# Stock Price Prediction with PyTorch  [LSTM vs GRU (DJIA 30 Stock Time Series)]

Bu proje, **Microsoft AI Summer School** programı kapsamında geliştirilmiştir. Kaggle DJIA 30 Stock Time Series veri seti kullanılarak tekil hisse senedi (varsayılan: **AAPL**) fiyat tahmini üzerine gerçekleştirilen bir zaman serisi regresyon çalışmasıdır.

Hibrit NLP/Sentiment projelerinden bağımsız olarak bu depo, saf zaman serisi mimarilerinin performansına odaklanır özellikle PyTorch ile implement edilen **LSTM (Long Short-Term Memory)** ve **GRU (Gated Recurrent Unit)** modellerini karşılaştırır.

---

## 📂 Proje Yapısı

```text
Stock_Price_Prediction/
├── stock price predicton with pytorch.ipynb  # Kodları, grafikleri ve analizleri içeren ana Notebook
├── data/
│   ├── AAPL_2006-01-01_to_2018-01-01.csv       # Tarihsel Apple hisse senedi veri seti
│   ├── all_stocks_2006-01-01_to_2018-01-01.csv # Tüm DJIA 30 veri seti (2006-2018)
│   ├── all_stocks_2017-01-01_to_2018-01-01.csv # Tüm DJIA 30 veri seti (2017-2018)
│   └── results_summary.csv                     # Kaydedilen model performans metrikleri
└── README.md                                   # Proje dokümantasyonu
