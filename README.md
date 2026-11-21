# Employee Attrition Prediction

Đồ án cuối môn **Nhập môn Phân tích dữ liệu và Học sâu**: dự đoán nguy cơ nghỉ việc của nhân viên từ bộ dữ liệu **IBM HR Analytics Employee Attrition**.

---

## 1. Giới thiệu

Dự án xây dựng, đánh giá và so sánh các mô hình dự đoán tình trạng nghỉ việc (`Attrition`) của nhân viên dựa trên dữ liệu nhân sự.

Các mô hình đã triển khai:

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
| Python 3.13.3 | Ngôn ngữ lập trình (notebook 06 dùng f-string lồng dấu nháy kép nên cần Python ≥ 3.12) |
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

### Phiên bản đã ghi nhận khi chạy notebook

| Thư viện | Phiên bản |
|---|---|
| Python (kernel `.venv`) | 3.13.3 |
| pandas | 3.1.1 |
| NumPy | 2.5.4 |
| scikit-learn | 1.9.1 |
| TensorFlow | 2.21.0 |
| CatBoost, SHAP | Chưa được ghi lại trong output; chạy `python -m pip freeze` trong `.venv` để lấy phiên bản |

Các phiên bản trên lấy từ output thực tế của notebook, dùng để đối chiếu khi gặp lỗi tương thích.

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
│   ├── logistic_regression_pipeline.pkl
│   ├── catboost_model.cbm
│   └── employee_attrition_mlp.keras
│
├── results/
│   ├── ml_model_comparison.csv
│   ├── ml_predictions.csv
│   ├── catboost_feature_importance.csv
│   ├── mlp_model_results.csv
│   ├── mlp_predictions.csv
│   ├── all_model_comparison.csv
│   ├── model_ranking_by_f1.csv
│   ├── best_model_by_metric.csv
│   ├── catboost_shap_importance.csv
│   └── plots/
│       ├── catboost_shap_bar.png
│       └── catboost_shap_beeswarm.png
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
| `03_data_preprocessing.ipynb` | Loại bỏ cột không cần thiết, mã hóa target, chia train/test, One-Hot Encoding, scaling và kiểm tra dữ liệu sau xử lý (không lưu dữ liệu đã xử lý ra file) |
| `04_machine_learning.ipynb` | Huấn luyện và đánh giá Logistic Regression, CatBoost |
| `05_deep_learning.ipynb` | Xây dựng, huấn luyện và đánh giá MLP |
| `06_model_evaluation.ipynb` | Gộp kết quả 3 mô hình, bảng so sánh và xếp hạng, ROC/PR curves chung, SHAP (beeswarm, bar, waterfall) cho CatBoost |

### Thư mục đầu ra

- `models/`: lưu mô hình đã huấn luyện và pipeline.
- `results/`: lưu metrics, dự đoán, feature importance và các kết quả phân tích.
- `report/`: lưu báo cáo cuối kỳ, hình ảnh và tài liệu liên quan.

| Notebook ghi file | File tạo ra |
|---|---|
| `04_machine_learning.ipynb` | `results/ml_model_comparison.csv`, `results/catboost_feature_importance.csv`, `results/ml_predictions.csv`, `models/logistic_regression_pipeline.pkl`, `models/catboost_model.cbm` |
| `05_deep_learning.ipynb` | `results/mlp_model_results.csv`, `results/mlp_predictions.csv`, `models/employee_attrition_mlp.keras` |
| `06_model_evaluation.ipynb` | `results/all_model_comparison.csv`, `results/model_ranking_by_f1.csv`, `results/best_model_by_metric.csv`, `results/catboost_shap_importance.csv`, `results/plots/catboost_shap_bar.png`, `results/plots/catboost_shap_beeswarm.png` |

Notebook 01, 02 và 03 không ghi file đầu ra. Biểu đồ SHAP waterfall chỉ hiển thị trong notebook, chưa được lưu thành file.

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

Các Notebook dùng `Path.cwd().parent` làm thư mục gốc, nên phải chạy với thư mục làm việc là `notebooks/` (mặc định của VS Code khi mở Notebook từ thư mục này).

### Phụ thuộc giữa các Notebook

| Notebook | Cần gì trước khi chạy |
|---|---|
| 01, 02, 03 | Chỉ cần file CSV trong `dataset/` |
| 04 | Chỉ cần file CSV (tự tiền xử lý và chia dữ liệu lại, không đọc kết quả của 03) |
| 05 | Chỉ cần file CSV (tự tiền xử lý và chia dữ liệu lại, không đọc kết quả của 03) |
| 06 | **Bắt buộc chạy xong 04 và 05**: đọc `results/ml_model_comparison.csv`, `results/mlp_model_results.csv`, `results/ml_predictions.csv`, `results/mlp_predictions.csv` và `models/catboost_model.cbm` |

Vì 04 và 05 đều tạo lại train/test split bằng cùng cấu hình (`test_size=0.2`, `random_state=42`, `stratify=y`), nếu thay đổi cách chia dữ liệu thì phải đổi đồng bộ ở cả 03, 04 và 05.

### Đầu ra dự kiến theo giai đoạn

| Giai đoạn | Đầu ra |
|---|---|
| Data Collection | Dataset được tải, đọc và kiểm tra |
| EDA | Thống kê, biểu đồ phân bố và phân tích dữ liệu |
| Preprocessing | Kiểm tra shape, missing/infinite values và scaling của dữ liệu đã xử lý (chỉ hiển thị trong Notebook, chưa lưu ra file) |
| Machine Learning | Metrics, classification reports, predictions, model files và CatBoost feature importance |
| Deep Learning | MLP, training history, metrics, predictions và model file |
| Model Evaluation | Bảng so sánh, xếp hạng, ROC/PR curves chung và SHAP |
| Final Report | Báo cáo phương pháp, kết quả, thảo luận, hạn chế và kết luận |

### Tóm tắt kết quả EDA

Số liệu lấy từ output của `02_data_exploration.ipynb`. Đây là các mối liên hệ thống kê mô tả, không chứng minh quan hệ nhân quả.

| Đặc trưng | Quan sát |
|---|---|
| OverTime | Làm thêm giờ: 30,53% nghỉ việc; không làm thêm giờ: 10,44% |
| JobRole | Sales Representative có tỷ lệ nghỉ việc cao nhất trong các nhóm đã tổng hợp (39,76%) |
| MaritalStatus | Single: 25,53% |
| Department | Sales 20,63%, Human Resources 19,05%, Research & Development 13,84% |
| JobSatisfaction | Mức 1: 22,84%; mức 4: 11,33% |
| Gender | Nam 17,01%, nữ 14,80% |
| Age | Trung bình 33,61 (nghỉ việc) so với 37,56 (ở lại) |
| MonthlyIncome | Trung vị 3.202 (nghỉ việc) so với 5.204 (ở lại) |
| YearsAtCompany | Trung vị 3 năm (nghỉ việc) so với 6 năm (ở lại) |
| DistanceFromHome | Trung bình 10,63 (nghỉ việc) so với 8,92 (ở lại) |

Năm đặc trưng có Feature Importance cao nhất của CatBoost (`04_machine_learning.ipynb`): JobRole (7,66), OverTime (6,82), Age (5,71), MonthlyIncome (4,96), NumCompaniesWorked (4,58).

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

## 11. Kết quả thực nghiệm

Stage 5 đã triển khai Logistic Regression và CatBoost trên cùng train/test split với cấu hình baseline.

### Baseline – Machine Learning

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

### Cấu hình thực nghiệm

| Hạng mục | Cấu hình ghi nhận từ Notebook |
|---|---|
| Cột bị loại | `EmployeeNumber`, `EmployeeCount`, `Over18`, `StandardHours` (35 cột còn 31 cột, gồm 30 feature và `Attrition`) |
| Target | `No` = 0, `Yes` = 1 |
| Feature | 7 categorical, 23 numerical |
| Train/Test split | 80/20, `random_state=42`, `stratify=y`: train 1.176 dòng (986 No / 190 Yes), test 294 dòng (247 No / 47 Yes) |
| Tiền xử lý cho Logistic Regression và MLP | `OneHotEncoder(handle_unknown="ignore")` + `StandardScaler`, tạo 51 feature |
| Tiền xử lý cho CatBoost | Giữ dữ liệu gốc, khai báo `cat_features` |
| Logistic Regression | `LogisticRegression(max_iter=1000, random_state=42)` trong Pipeline cùng preprocessing; không dùng `class_weight` |
| CatBoost | `iterations=500`, `depth=6`, `learning_rate=0.03`, `Logloss`, `eval_metric=AUC`, `random_seed=42`; không dùng trọng số lớp |
| MLP | Dense 128 → Dropout 0.3 → Dense 64 → Dropout 0.3 → Dense 32 → Dense 1 (sigmoid), 17.025 tham số; Adam (`learning_rate=0.001`), `binary_crossentropy`, `batch_size=32`, tối đa 100 epoch |
| MLP: validation | Tách 15% từ train: 999 mẫu train, 177 mẫu validation |
| MLP: callbacks | `EarlyStopping` (theo `val_loss`, `patience=10`, khôi phục weights tốt nhất), `ReduceLROnPlateau` (`factor=0.5`, `patience=5`, `min_lr=0.00001`) |
| MLP: xử lý mất cân bằng | `class_weight` = {0: 0,596, 1: 3,102} |
| Ngưỡng phân loại | 0.5 cho cả ba mô hình |

### Kết quả MLP và so sánh ba mô hình

Bảng dưới lấy từ output của `06_model_evaluation.ipynb` (đọc từ các file CSV trong `results/`), sắp xếp theo F1-score:

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| MLP Neural Network | 0.8537 | 0.5417 | 0.5532 | 0.5474 | 0.7893 | 0.5330 |
| Logistic Regression | 0.8605 | 0.6154 | 0.3404 | 0.4384 | 0.8115 | 0.5836 |
| CatBoost | 0.8537 | 0.6667 | 0.1702 | 0.2712 | 0.8118 | 0.5327 |

> **Lưu ý về MLP:** output đang lưu trong `05_deep_learning.ipynb` là một lần chạy khác (Accuracy 0.8503, Precision 0.5294, Recall 0.5745, F1-score 0.5510, ROC-AUC 0.7868, PR-AUC 0.5409; huấn luyện dừng ở epoch 28, khôi phục weights của epoch 18). Hai lần chạy MLP cho kết quả lệch nhau dù đã đặt seed, nên các con số của MLP chỉ nên dùng như một lần chạy cụ thể. Cần chạy lại 05 và 06 sau khi cố định seed (xem phần "Vấn đề đã biết và việc cần làm") trước khi đưa số liệu cuối vào báo cáo.

Nhận xét:

- MLP có Recall và F1-score cao nhất, nhưng MLP dùng `class_weight` còn Logistic Regression và CatBoost thì không, nên so sánh này chưa hoàn toàn công bằng.
- Logistic Regression cao nhất ở Accuracy và PR-AUC; CatBoost cao nhất ở Precision và ROC-AUC (chênh lệch ROC-AUC với Logistic Regression chỉ 0.0003).
- Tập test chỉ có 47 mẫu thuộc lớp nghỉ việc, nên chênh lệch nhỏ giữa các mô hình có thể không có ý nghĩa thống kê.

---

## 12. Reproducibility và tránh Data Leakage

Để tăng tính công bằng khi so sánh mô hình:

- Sử dụng `random_state=42` cho các bước chia dữ liệu có hỗ trợ tham số này.
- Notebook 04 và 05 cùng gọi `train_test_split(test_size=0.2, random_state=42, stratify=y)` trên cùng `X`, `y`, nên cùng một tập test 294 dòng và cùng thứ tự. File predictions hiện không lưu chỉ số dòng, và notebook 06 chưa có bước kiểm tra tự động rằng cột `Actual` của hai file khớp nhau.
- Hiện chưa tuning hyperparameters và chưa chọn threshold; cả ba mô hình dùng ngưỡng 0.5 và cấu hình cố định. Không sử dụng test set để tuning hoặc chọn threshold khi bổ sung các bước này.
- Fit preprocessing trên dữ liệu train, sau đó mới transform test. Với MLP, validation được tách ra sau khi `fit_transform` trên toàn bộ train, nên scaler/encoder đã học cả phần validation; ảnh hưởng nhỏ nhưng cần ghi nhận.
- Với Deep Learning, sử dụng validation set để theo dõi quá trình training và Early Stopping.
- Chỉ MLP dùng `class_weight`; Logistic Regression và CatBoost chưa xử lý mất cân bằng lớp. Cần ghi rõ điều này khi so sánh Recall và F1-score.
- Lưu cấu hình, metrics và output của các lần thử nghiệm để có thể đối chiếu.

> Việc cố định random seed giúp tái lập một phần kết quả, nhưng không đảm bảo mọi môi trường phần cứng hoặc phiên bản thư viện sẽ tạo ra kết quả hoàn toàn giống nhau.

> Notebook 05 mới gọi `np.random.seed(42)` và `tf.random.set_seed(42)`. Kết quả MLP lưu trong `results/` và output hiện có của notebook 05 khác nhau, nên cần cố định seed chặt hơn (xem phần "Vấn đề đã biết và việc cần làm").

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

### Notebook 06 báo `FileNotFoundError` hoặc `SyntaxError`

- `FileNotFoundError` khi đọc `results/*.csv` hoặc `models/catboost_model.cbm`: chạy xong notebook 04 và 05 trước.
- `SyntaxError` ở cell Precision-Recall curve: Python < 3.12 không cho dùng cùng loại dấu nháy lồng trong f-string. Dùng Python 3.12 trở lên hoặc đổi dấu nháy bên trong f-string.

### Cảnh báo `Pandas4Warning` khi dùng `select_dtypes(include=["object"])`

Với pandas 3.x, cảnh báo này xuất hiện ở notebook 02, 03, 04, 05 và 06. Kết quả vẫn đúng; có thể bỏ cảnh báo bằng cách dùng `include=["object", "string"]`.

### Cảnh báo TensorFlow không hỗ trợ GPU trên Windows

Từ TensorFlow 2.11, bản native Windows chỉ chạy trên CPU. Đây là cảnh báo, không phải lỗi; MLP của dự án đủ nhỏ để huấn luyện bằng CPU.

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
| 3 | Exploratory Data Analysis (EDA) | Hoàn thành (Notebook 02 có đầy đủ output) |
| 4 | Data Preprocessing | Hoàn thành và đã kiểm tra output; dữ liệu đã xử lý chưa được lưu ra file (04 và 05 tự tiền xử lý lại) |
| 5 | Machine Learning | Hoàn thành baseline Logistic Regression và CatBoost; đã lưu model và kết quả |
| 6 | Deep Learning (MLP) | Hoàn thành huấn luyện, đánh giá và lưu model/kết quả; cần cố định seed để tái lập |
| 7 | Model Evaluation & Explainability (SHAP) | Đã có code đầy đủ; Notebook 06 chỉ còn output ở phần lưu SHAP plots và xếp hạng, cần chạy lại toàn bộ để lưu output |
| 8 | Final Report | Chưa thực hiện |

---

## 16. Stage 7 – Model Evaluation & Explainability

### Objectives

- Compare Logistic Regression, CatBoost, and MLP using a unified metrics table.
- Visualize Accuracy, Precision, Recall, F1-score, ROC-AUC, and PR-AUC.
- Compare ROC and Precision-Recall curves using prediction probabilities from the same test split.
- Explain CatBoost predictions with SHAP, including global feature importance and individual predictions.

### Nội dung notebook `06_model_evaluation.ipynb`

- Đọc kết quả từ `results/` (Stage 5 và Stage 6), chuẩn hóa tên cột và gộp thành bảng so sánh 3 mô hình.
- Tìm mô hình tốt nhất theo từng metric; biểu đồ cột cho toàn bộ metric, riêng Recall và F1-score.
- ROC curve và Precision-Recall curve chung cho 3 mô hình, tính từ `ml_predictions.csv` và `mlp_predictions.csv`.
- SHAP cho CatBoost: beeswarm, bar plot (mean absolute SHAP), waterfall cho một mẫu.
- Xếp hạng mô hình theo F1-score và lưu kết quả.

### Đầu ra

- `results/all_model_comparison.csv`, `results/best_model_by_metric.csv`, `results/model_ranking_by_f1.csv`
- `results/catboost_shap_importance.csv`
- `results/plots/catboost_shap_bar.png`, `results/plots/catboost_shap_beeswarm.png`

### Lưu ý khi diễn giải SHAP

- SHAP được tính trên 300 dòng lấy ngẫu nhiên (`random_state=42`) từ **toàn bộ** dataset, bao gồm cả các dòng CatBoost đã dùng để huấn luyện. Kết quả mô tả cách mô hình sử dụng đặc trưng, không phải đánh giá trên dữ liệu chưa thấy.
- Biểu đồ waterfall giải thích dòng đầu tiên của mẫu SHAP, không phải một dòng được chọn từ tập test.
- SHAP chỉ áp dụng cho CatBoost, mô hình có Recall và F1-score thấp nhất ở ngưỡng 0.5. Mô hình có F1-score cao nhất (MLP) chưa được giải thích bằng SHAP.
- SHAP phản ánh đóng góp của đặc trưng vào dự đoán của mô hình, không chứng minh quan hệ nhân quả.

### Vấn đề đã biết và việc cần làm

1. **Chạy lại toàn bộ notebook 06** (Run All) để lưu output của tất cả cell; hiện chỉ các cell lưu SHAP plots và xếp hạng còn output. Notebook này cũng chưa có kernel metadata.
2. **Cố định seed cho MLP** trước khi báo cáo số liệu: thêm `tf.keras.utils.set_random_seed(42)` và `tf.config.experimental.enable_op_determinism()` ở đầu notebook 05, chạy lại 05 rồi 06 để `results/` và output khớp nhau. Có thể chạy nhiều seed và báo cáo trung bình ± độ lệch chuẩn.
3. **Kiểm tra cùng tập test** trong notebook 06 trước khi vẽ đường cong chung, ví dụ: `assert (ml_predictions["Actual"].values == mlp_predictions["Actual"].values).all()`.
4. **Lưu preprocessor của MLP** (ví dụ bằng `joblib.dump(preprocessor, ...)` trong notebook 05). File `employee_attrition_mlp.keras` chỉ chứa mạng nơ-ron; không có preprocessor thì không thể dự đoán trên dữ liệu thô.
5. **Cân bằng điều kiện so sánh**: thử `class_weight="balanced"` cho Logistic Regression và `auto_class_weights="Balanced"` cho CatBoost, hoặc nêu rõ trong báo cáo rằng chỉ MLP có xử lý mất cân bằng lớp.
6. **Phân tích threshold** (đã dự kiến ở phần giới thiệu Stage 7) chưa được triển khai. Nếu thực hiện, chọn threshold trên validation hoặc bằng cross-validation, không chọn trên test set.
7. Sửa lỗi nhỏ: notebook 03 in toàn bộ `y_test` thay vì `y_test.shape` ở cell chia train/test.

Stage 7 chỉ được đánh dấu hoàn thành sau khi các cell được chạy lại, output được kiểm tra và các mục trên được xử lý hoặc ghi rõ là hạn chế của đồ án.

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
