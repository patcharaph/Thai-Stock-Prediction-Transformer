# 📈 Thai Stock Prediction with LSTM & Transformer

โปรเจกต์นี้เป็นการทดลองสร้างโมเดล AI เพื่อทำนายราคาดัชนี SET50 โดยใช้โมเดล LSTM เป็น Benchmark และเปรียบเทียบประสิทธิภาพกับโมเดล Transformer

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
จากการทดลอง, โมเดล Transformer สามารถลดค่าความผิดพลาด (RMSE) ลงได้ X% เมื่อเทียบกับ LSTM Benchmark

| Model       | RMSE  |
|-------------|-------|
| LSTM        | 22.859689 |
| Transformer | 255.930063 |

**กราฟเปรียบเทียบผลการทำนาย:**

![Prediction Result](<img width="1473" height="781" alt="image" src="https://github.com/user-attachments/assets/0dbcdf3a-49d7-46c9-a785-3399a140dff5" />
)


*(คุณจะต้องสร้างโฟลเดอร์ images แล้วนำภาพ Screenshot ของกราฟผลลัพธ์จาก Notebook ที่ 4 มาใส่)*

## 🔮 แนวทางการพัฒนาต่อ (Future Work)
- เพิ่มข้อมูล Sentiment Analysis จากข่าวมาเป็น Feature
- ทดลองกับหุ้นรายตัว
- นำโมเดลที่ดีที่สุดไปสร้างเป็น Dashboard ด้วย Streamlit
