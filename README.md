# 📈 Thai Stock Prediction with LSTM & Transformer

โปรเจกต์นี้เป็นการทดลองสร้างโมเดล AI เพื่อทำนายราคาดัชนี SET โดยใช้โมเดล LSTM เป็น Benchmark และเปรียบเทียบประสิทธิภาพกับโมเดล Transformer

## 🛠️ Tech Stack & Libraries
- Python 3.x
- Google Colab (for GPU training)
- TensorFlow / Keras
- Pandas & Pandas-TA
- Scikit-learn
- yfinance
- Matplotlib

## 📂 โครงสร้างโปรเจกต์ (Project Structure)
Thai-Stock-Prediction-Transformer/
├── 01_notebooks/             # โค้ดทั้งหมดในรูปแบบ Jupyter Notebooks
│   ├── 1_Data_Preparation.ipynb
│   ├── 2_LSTM_Benchmark_Training.ipynb
│   ├── 3_Transformer_Upgrade_Training.ipynb
│   └── 4_Model_Comparison.ipynb
|   |__ 4.1_SET50_Model_Comparison_Fixed
├── 02_data/                  # โฟลเดอร์สำหรับข้อมูล (ถูก gitignore)
├── 03_models/                # โฟลเดอร์สำหรับโมเดล (ถูก gitignore)
├── .gitignore
├── LICENSE
└── README.md


## 🚀 วิธีการรันโปรเจกต์ (How to Run)
1. Clone repository นี้ลงบนเครื่องของคุณ: `git clone <URL>`
2. เปิดโฟลเดอร์ `01_notebooks/`
3. รัน Notebook ตามลำดับตั้งแต่ `1_...` ถึง `4_...` บน Google Colab หรือ Jupyter Environment ของคุณ
   - Notebook `1_Data_Preparation.ipynb` จะทำการดึงข้อมูลและสร้างไฟล์ `set50_processed_data.csv` ในโฟลเดอร์ `02_data/`
   - Notebooks `2_...` และ `3_...` จะใช้ข้อมูลนั้นเพื่อเทรนและบันทึกโมเดลลงในโฟลเดอร์ `03_models/`

## 📊 ผลลัพธ์ (Results)
จากการทดลอง, โมเดล Transformer 

Model	RMSE (Baht)	MAE (Baht)	Directional Acc.
LSTM (Benchmark)	24.7	20.2	53.5%
Transformer	96.5	68.3	49.5%

RMSE / MAE: LSTM ดีกว่า Transformer ชัดเจน (~4 เท่า) → LSTM ทายระดับราคาได้แม่นกว่า

Directional Accuracy: LSTM ~53% (ดีกว่าทอยเหรียญเล็กน้อย), Transformer ~49% (ใกล้ random)

กราฟก็สะท้อนว่า Transformer “หลุดเทรนด์” ในช่วงหลัง

**ทำไม Transformer แพ้ LSTM ในที่นี้?

1. Data size (2392 แถว ≈ 9 ปี) → ไม่ใหญ่มากสำหรับ Transformer ที่พารามิเตอร์เยอะ
→ LSTM ทำงานดีกว่าเมื่อข้อมูลไม่เยอะและ pattern ไม่ซับซ้อนมาก

2. Hyperparameters ของ Transformer

ff_dim=128, blocks=3 → อาจใหญ่ไปสำหรับฟีเจอร์ ~15 ตัว

ไม่มี regularization เพียงพอ → เริ่ม overfit → ผลบน test แย่

3. Feature set → ตอนนี้ใช้เพียง indicator standard (RSI, MACD, BBands)

ถ้าเพิ่มฟีเจอร์ engineered (returns, rolling stats, volume-based) → Transformer จะได้เปรียบมากขึ้น

4. Label = ราคาปิด (Close) → มี non-stationary สูง

LSTM เก่งกว่าในการเรียนรู้การเลื่อนไปทีละสเต็ป

Transformer มักเหมาะกับ sequence ยาวๆ + stationary (เช่น return series)

**กราฟเปรียบเทียบผลการทำนาย:**

![Prediction Result](https://drive.google.com/file/d/16oUPDAkN_14dWJ_2lEpE70dGcP8h8-QQ/view?usp=drive_link)


## 🔮 แนวทางการพัฒนาต่อ (Future Work)
- เพิ่มข้อมูล Sentiment Analysis จากข่าวมาเป็น Feature
- ทดลองกับหุ้นรายตัว
- นำโมเดลที่ดีที่สุดไปสร้างเป็น Dashboard ด้วย Streamlit
