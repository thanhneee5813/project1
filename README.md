# Employee Attrition Prediction

Đồ án cuối môn **Nhập môn Phân tích dữ liệu và Học sâu**: dự đoán nguy cơ nghỉ việc của nhân viên từ bộ dữ liệu **IBM HR Analytics Employee Attrition**.

---

## 1. Giới thiệu

Dự án xây dựng, đánh giá và so sánh các mô hình dự đoán tình trạng nghỉ việc (`Attrition`) của nhân viên dựa trên dữ liệu nhân sự.

Các mô hình dự kiến triển khai:

- Logistic Regression
- CatBoost
- Deep Learning MLP (Multilayer Perceptron)

Ngoài đánh giá hiệu suất dự đoán, dự án sử dụng **SHAP** để giải thích mức độ đóng góp của các đặc trưng vào dự đoán của mô hình.

> **Giới hạn dữ liệu:** IBM HR Analytics Employee Attrition là bộ dữ liệu mô phỏng. Kết quả phân tích không đại diện cho mọi doanh nghiệp, không chứng minh quan hệ nhân quả và không nên được sử dụng như căn cứ duy nhất cho quyết định nhân sự thực tế.

### Mục tiêu

- Khám phá các đặc điểm và phân bố trong dữ liệu nhân sự.
- Phân tích các yếu tố có liên quan đến tình trạng nghỉ việc.
- Tiền xử lý dữ liệu phục vụ mô hình.
- Xây dựng và so sánh các mô hình Machine Learning và Deep Learning.
- Đánh giá mô hình bằng nhiều chỉ số, đặc biệt chú ý đến khả năng phát hiện nhóm nghỉ việc.
- Sử dụng SHAP để diễn giải mô hình và đặc trưng quan trọng.

---

## 2. Dataset

**Dataset:** IBM HR Analytics Employee Attrition  
**Nguồn:** Kaggle – IBM HR Analytics Attrition Dataset

Link: https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset

Dataset có 1.470 dòng và 35 cột trong lần kiểm tra ban đầu.

| Thông tin | Giá trị ghi nhận ban đầu |
|---|---:|
| Số dòng | 1.470 |
| Số cột | 35 |
| Missing values | 0 |
| Duplicate rows | 0 |
| Attrition = No | 1.233 |
| Attrition = Yes | 237 |

Tỷ lệ nhãn ban đầu:

- No (ở lại): khoảng 83,88%
- Yes (nghỉ việc): khoảng 16,12%

Dataset có sự mất cân bằng giữa hai lớp. Vì vậy, không đánh giá mô hình chỉ dựa trên Accuracy; cần xem thêm Precision, Recall, F1-score và PR-AUC.

### Tải và chuẩn bị dữ liệu

1. Mở trang Kaggle và đăng nhập nếu cần.
2. Tải dataset về máy.
3. Giải nén file ZIP.
4. Đặt file CSV trong thư mục `dataset/` ở thư mục gốc dự án.
5. Đảm bảo tên file:

```text
WA_Fn-UseC_-HR-Employee-Attrition.csv
```

Cấu trúc mong đợi:

```text
Employee-Attrition-Prediction/
└── dataset/
    └── WA_Fn-UseC_-HR-Employee-Attrition.csv
```

Không đưa dữ liệu cá nhân hoặc dữ liệu nhân viên thực tế, nhạy cảm vào repository công khai.

---

## 3. Công nghệ sử dụng

| Công nghệ | Mục đích |
|---|---|
| Python 3.13.3 | Ngôn ngữ lập trình |
| Visual Studio Code | IDE |
| Jupyter Notebook | Thực hiện từng giai đoạn phân tích và xây dựng mô hình |
| Pandas | Đọc, xử lý và phân tích dữ liệu |
| NumPy | Tính toán số học |
| Matplotlib | Trực quan hóa |
| Seaborn | Trực quan hóa dữ liệu thống kê |
| Scikit-learn | Preprocessing, Logistic Regression và đánh giá |
| CatBoost | Mô hình Gradient Boosting hỗ trợ dữ liệu categorical |
| TensorFlow / Keras | Xây dựng và huấn luyện MLP |
| SHAP | Giải thích mô hình |
| Joblib | Lưu pipeline/model hỗ trợ |

Các thư viện bổ sung sẽ được cài đặt khi đến giai đoạn sử dụng tương ứng.

---

## 4. Cấu trúc thư mục

```text
Employee-Attrition-Prediction/
│
├── dataset/
│   └── WA_Fn-UseC_-HR-Employee-Attrition.csv
│
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_data_exploration.ipynb
│   ├── 03_data_preprocessing.ipynb
│   ├── 04_machine_learning.ipynb
│   ├── 05_deep_learning.ipynb
│   └── 06_model_evaluation.ipynb
│
├── models/
│   └── (các model sau khi huấn luyện)
│
├── results/
│   └── (metrics, predictions, feature importance và kết quả)
│
├── report/
│   └── (báo cáo đồ án và tài liệu)
│
├── .venv/
├── .gitignore
├── requirements.txt
└── README.md
```

### Ý nghĩa các Notebook

| Notebook | Nội dung |
|---|---|
| `01_data_collection.ipynb` | Đọc dataset, kiểm tra kích thước, kiểu dữ liệu, missing values, duplicate và phân bố target ban đầu |
| `02_data_exploration.ipynb` | EDA, thống kê và trực quan hóa dữ liệu |
| `03_data_preprocessing.ipynb` | Làm sạch, loại bỏ cột không cần thiết, encoding, scaling và chia dữ liệu |
| `04_machine_learning.ipynb` | Huấn luyện và đánh giá Logistic Regression, CatBoost |
| `05_deep_learning.ipynb` | Xây dựng, huấn luyện và đánh giá MLP |
| `06_model_evaluation.ipynb` | So sánh các mô hình, đánh giá sâu, threshold và giải thích mô hình bằng SHAP |

### Thư mục đầu ra

- `models/`: lưu mô hình đã huấn luyện và pipeline.
- `results/`: lưu metrics, dự đoán, feature importance và các kết quả phân tích.
- `report/`: lưu báo cáo cuối kỳ, hình ảnh và tài liệu liên quan.

---

## 5. Yêu cầu trước khi chạy

1. Windows 10/11 (các lệnh bên dưới sử dụng PowerShell).
2. Python 3.13.3 được cài đặt và có thể gọi bằng lệnh `python`.
3. Visual Studio Code.
4. Extension trong VS Code:
   - Python (Microsoft)
   - Jupyter (Microsoft)

Kiểm tra Python:

```powershell
python --version
```

Phiên bản môi trường ban đầu:

```text
Python 3.13.3
```

---

## 6. Cài đặt môi trường

### Bước 1: Mở dự án

Mở thư mục `Employee-Attrition-Prediction` bằng VS Code.

Mở Terminal: **Terminal → New Terminal**. Đảm bảo terminal đang ở thư mục gốc dự án.

### Bước 2: Tạo virtual environment

Thực hiện một lần:

```powershell
python -m venv .venv
```

### Bước 3: Kích hoạt virtual environment

```powershell
.\.venv\Scripts\Activate.ps1
```

Nếu PowerShell chặn script, chạy trong terminal hiện tại:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Sau đó kích hoạt lại:

```powershell
.\.venv\Scripts\Activate.ps1
```

Khi thành công, đầu dòng terminal sẽ hiển thị tiền tố `(.venv)`.

### Bước 4: Cập nhật pip

```powershell
python -m pip install --upgrade pip
```

### Bước 5: Cài thư viện từ requirements.txt

```powershell
python -m pip install -r requirements.txt
```

Nếu `requirements.txt` chưa có hoặc bạn muốn cài thư viện cơ bản trước:

```powershell
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter ipykernel
```

Các thư viện bổ sung như CatBoost, TensorFlow và SHAP được khai báo trong `requirements.txt` khi cần cho các giai đoạn tương ứng.

### Bước 6: Đăng ký Jupyter Kernel

```powershell
python -m ipykernel install --user --name employee-attrition --display-name "Python (Employee Attrition)"
```

### Bước 7: Kiểm tra môi trường

```powershell
python -c "import pandas, numpy, matplotlib, seaborn, sklearn; print('Environment OK')"
```

Nếu hiển thị `Environment OK`, các thư viện cơ bản đã import thành công.

---

## 7. requirements.txt

Tạo file `requirements.txt` ở thư mục gốc dự án. Danh sách package dự kiến cho các giai đoạn:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
jupyter
ipykernel
catboost
tensorflow
shap
joblib
```

Cài đặt:

```powershell
python -m pip install -r requirements.txt
```

> Danh sách trên là dependency dự kiến của dự án, không phải file khóa phiên bản. Nếu gặp lỗi tương thích, kiểm tra phiên bản Python/package và cập nhật dependency phù hợp với môi trường đang sử dụng. Khi dự án ổn định, có thể tạo file khóa phiên bản để tăng khả năng tái lập.

---

## 8. Chọn Kernel trong VS Code

1. Mở Notebook cần chạy trong thư mục `notebooks/`.
2. Nhấn **Select Kernel** ở góc trên bên phải.
3. Chọn **Python (Employee Attrition)**.
4. Kiểm tra Python trong một cell:

```python
import sys

print(sys.version)
```

Kernel cần sử dụng đúng virtual environment của dự án.

---

## 9. Quy trình chạy dự án

Chạy Notebook theo thứ tự:

1. `01_data_collection.ipynb`
2. `02_data_exploration.ipynb`
3. `03_data_preprocessing.ipynb`
4. `04_machine_learning.ipynb`
5. `05_deep_learning.ipynb`
6. `06_model_evaluation.ipynb`

Trong mỗi Notebook:

1. Chọn đúng Kernel `Python (Employee Attrition)`.
2. Chạy cell tuần tự bằng **Run Cell** hoặc `Shift + Enter`.
3. Kiểm tra output và xử lý lỗi trước khi chạy tiếp.
4. Lưu Notebook bằng `Ctrl + S`.

Không nên chạy các Notebook sau khi chưa hoàn thành và kiểm tra đầu ra cần thiết từ các bước trước.

### Đầu ra dự kiến theo giai đoạn

| Giai đoạn | Đầu ra |
|---|---|
| Data Collection | Dataset được tải, đọc và kiểm tra |
| EDA | Thống kê, biểu đồ phân bố và phân tích dữ liệu |
| Preprocessing | Dữ liệu train/test đã được xử lý cho mô hình |
| Machine Learning | Metrics, classification reports, predictions, model files và CatBoost feature importance |
| Deep Learning | MLP, training history, metrics, predictions và model file |
| Model Evaluation | Bảng so sánh, ROC/PR curves, phân tích threshold và SHAP |
| Final Report | Báo cáo phương pháp, kết quả, thảo luận, hạn chế và kết luận |

---

## 10. Model Evaluation Metrics

Dự án sử dụng các chỉ số sau để đánh giá mô hình:

| Metric | Ý nghĩa |
|---|---|
| Accuracy | Tỷ lệ dự đoán đúng trên toàn bộ mẫu |
| Precision | Trong số các mẫu được dự đoán nghỉ việc, tỷ lệ thực sự nghỉ việc |
| Recall | Tỷ lệ nhân viên thực sự nghỉ việc được mô hình phát hiện |
| F1-score | Trung bình điều hòa Precision và Recall |
| ROC-AUC | Khả năng phân biệt giữa nhóm nghỉ việc và ở lại trên nhiều threshold |
| PR-AUC (Average Precision) | Đánh giá Precision/Recall, hữu ích khi dữ liệu mất cân bằng |

Do nhóm Attrition = Yes chiếm tỷ lệ thấp, **không nên chỉ dựa vào Accuracy**. Recall, F1-score và PR-AUC cần được quan tâm khi đánh giá khả năng phát hiện nhân viên nghỉ việc.

---

## 11. Baseline Results – Machine Learning

Stage 5 đã triển khai Logistic Regression và CatBoost trên cùng train/test split với cấu hình baseline.

### Kết quả lần chạy baseline

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8605 | 0.6154 | 0.3404 | 0.4384 | 0.8115 | 0.5836 |
| CatBoost | 0.8537 | 0.6667 | 0.1702 | 0.2712 | 0.8118 | 0.5327 |

### Nhận xét baseline

- Logistic Regression đạt Recall, F1-score và PR-AUC cao hơn CatBoost trong lần chạy này.
- CatBoost có Precision cao hơn Logistic Regression.
- ROC-AUC của hai mô hình gần như tương đương.
- Logistic Regression đang là mô hình baseline tốt hơn tổng thể theo các chỉ số tập trung vào phát hiện nhóm nghỉ việc trong kết quả hiện tại.

Đây là kết quả của cấu hình baseline, chưa phải kết quả cuối cùng sau tuning, threshold optimization hoặc các phương pháp xử lý mất cân bằng khác.

---

## 12. Reproducibility và tránh Data Leakage

Để tăng tính công bằng khi so sánh mô hình:

- Sử dụng `random_state=42` cho các bước chia dữ liệu có hỗ trợ tham số này.
- Các mô hình được đánh giá trên cùng tập test khi có thể.
- Không sử dụng test set để tuning hyperparameters hoặc chọn threshold.
- Fit preprocessing trên dữ liệu train, sau đó mới transform validation/test.
- Với Deep Learning, sử dụng validation set để theo dõi quá trình training và Early Stopping.
- Lưu cấu hình, metrics và output của các lần thử nghiệm để có thể đối chiếu.

> Việc cố định random seed giúp tái lập một phần kết quả, nhưng không đảm bảo mọi môi trường phần cứng hoặc phiên bản thư viện sẽ tạo ra kết quả hoàn toàn giống nhau.

---

## 13. Xử lý lỗi thường gặp

### Không kích hoạt được `.venv`

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

### VS Code không thấy Kernel

Kích hoạt `.venv`, chạy:

```powershell
python -m pip install ipykernel
python -m ipykernel install --user --name employee-attrition --display-name "Python (Employee Attrition)"
```

Quay lại Notebook và chọn Kernel lại.

### Không tìm thấy file CSV

Kiểm tra:

- Dataset đã nằm trong `dataset/` chưa.
- Tên file có đúng không.
- Notebook đang chạy từ thư mục nào.

Kiểm tra thư mục làm việc:

```python
from pathlib import Path

print("Current working directory:", Path.cwd())
print("Files in current directory:", list(Path.cwd().iterdir()))
```

### ImportError hoặc thiếu thư viện

Đảm bảo đã kích hoạt `.venv`, sau đó cài package thiếu:

```powershell
python -m pip install ten-thu-vien
```

Thay `ten-thu-vien` bằng package cần cài.

### Lỗi cài CatBoost, TensorFlow hoặc SHAP

1. Xác nhận virtual environment đang được kích hoạt.
2. Kiểm tra phiên bản Python:

```powershell
python --version
```

3. Cập nhật pip:

```powershell
python -m pip install --upgrade pip
```

4. Đọc kỹ thông báo lỗi cài đặt và kiểm tra khả năng tương thích của package với Python hiện tại.
5. Không cài package vào một Python khác với Kernel đang chạy Notebook.

---

## 14. .gitignore

Tạo file `.gitignore` ở thư mục gốc để tránh đưa các file môi trường, cache và output không cần thiết lên Git.

```gitignore
# Virtual environment
.venv/

# Python cache
__pycache__/
*.py[cod]

# Jupyter
.ipynb_checkpoints/

# VS Code local settings
.vscode/

# OS files
.DS_Store
Thumbs.db

# Generated model files
models/*.pkl
models/*.cbm
models/*.keras

# Generated results (uncomment if results should not be tracked)
# results/
```

Dataset, model và kết quả có thể được quản lý riêng tùy mục đích chia sẻ repository. Trước khi public dự án, kiểm tra quyền phân phối dataset và không đưa dữ liệu nhạy cảm lên GitHub.

---

## 15. Project Progress

| Stage | Nội dung | Trạng thái |
|---|---|---|
| 1 | Problem Definition | Hoàn thành |
| 2 | Data Collection | Đã thực hiện và kiểm tra dataset |
| 3 | Exploratory Data Analysis (EDA) | Cần xác nhận hoàn tất Notebook và output |
| 4 | Data Preprocessing | Đã xây dựng code; cần xác nhận lần chạy hoàn chỉnh |
| 5 | Machine Learning | Hoàn thành baseline Logistic Regression và CatBoost |
| 6 | Deep Learning (MLP) | Đã xây dựng hướng dẫn/code; chưa xác nhận training hoàn tất |
| 7 | Model Evaluation & Explainability (SHAP) | Chưa thực hiện |
| 8 | Final Report | Chưa thực hiện |

---



---

## 16. Stage 7 – Model Evaluation & Explainability (In Progress)

### Objectives
- Compare Logistic Regression, CatBoost, and MLP using a unified metrics table.
- Visualize Accuracy, Precision, Recall, F1-score, ROC-AUC, and PR-AUC.
- Compare ROC and Precision-Recall curves using prediction probabilities from the same test split.
- Explain CatBoost predictions with SHAP, including global feature importance and individual predictions.

### Planned notebook sections
- Model comparison table and best model by metric
- Metric comparison charts, including Recall and F1-score
- Combined ROC and Precision-Recall curves
- SHAP global summary (beeswarm and bar plots)
- SHAP local explanation (waterfall plot)

### Expected outputs
- `results/all_model_comparison.csv`
- SHAP plots for global and individual explanations

Stage 7 is in progress. The analysis and plots must be run and reviewed before marking this stage complete. Confirm that prediction files from Stage 5 and Stage 6 refer to the same test rows and ordering before drawing combined curves.

## 17. README Update Guidelines

**README.md là tài liệu hướng dẫn cài đặt, chạy dự án và theo dõi tiến độ. File này phải được cập nhật cùng mỗi giai đoạn hoặc tính năng mới.**

Khi thêm hoặc thay đổi một tính năng/giai đoạn, cần cập nhật các nội dung liên quan:

1. Mô tả tính năng hoặc giai đoạn.
2. Thư viện mới và lệnh cài đặt cụ thể.
3. Notebook, file hoặc thư mục mới được tạo.
4. Cách cấu hình môi trường nếu có.
5. Hướng dẫn chạy và sử dụng.
6. Đầu ra dự kiến, kết quả thực tế và cách kiểm tra.
7. Lỗi thường gặp và cách khắc phục nếu phát sinh.
8. Cập nhật checklist tiến độ.

Không ghi kết quả hoặc lệnh chưa kiểm chứng như thể đã chạy thành công. Nếu dependency thay đổi, cập nhật `requirements.txt` và hướng dẫn cài đặt tương ứng.

---

## 18. References

- Kaggle – IBM HR Analytics Employee Attrition Dataset: https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset
- Scikit-learn Documentation: https://scikit-learn.org/stable/
- CatBoost Documentation: https://catboost.ai/docs/
- TensorFlow Documentation: https://www.tensorflow.org/
- SHAP Documentation: https://shap.readthedocs.io/

---

**Project:** Employee Attrition Prediction  
**Course:** Nhập môn Phân tích dữ liệu và Học sâu  
**Purpose:** Academic project / learning and experimentation
