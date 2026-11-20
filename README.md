# Employee Attrition Prediction

Đồ án cuối môn **Nhập môn Phân tích dữ liệu và Học sâu**: dự đoán nguy
cơ nghỉ việc của nhân viên từ bộ dữ liệu IBM HR Analytics Employee
Attrition.

## 1. Giới thiệu

Dự án xây dựng và so sánh các mô hình dự đoán tình trạng nghỉ việc
(`Attrition`) của nhân viên:

-   Logistic Regression
-   CatBoost
-   Deep Learning MLP (Multilayer Perceptron)

Sử dụng SHAP để giải thích các đặc trưng ảnh hưởng đến dự đoán của mô
hình.

> Lưu ý: IBM HR Analytics Employee Attrition là bộ dữ liệu mô phỏng. Kết
> quả phân tích không đại diện cho mọi doanh nghiệp và không chứng minh
> quan hệ nhân quả.

## 2. Công nghệ sử dụng

-   Python 3.13.3
-   Visual Studio Code
-   Jupyter Notebook
-   Pandas, NumPy
-   Matplotlib, Seaborn
-   Scikit-learn
-   Các thư viện bổ sung như CatBoost, TensorFlow/Keras và SHAP sẽ được
    cài khi triển khai các giai đoạn tương ứng.

## 3. Cấu trúc thư mục

``` text
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
├── results/
├── report/
├── .venv/
└── README.md
```

Ý nghĩa các Notebook:

  -----------------------------------------------------------------------
  Notebook                            Nội dung
  ----------------------------------- -----------------------------------
  `01_data_collection.ipynb`          Đọc dữ liệu và kiểm tra dữ liệu ban
                                      đầu

  `02_data_exploration.ipynb`         Khám phá dữ liệu (EDA), thống kê và
                                      trực quan hóa

  `03_data_preprocessing.ipynb`       Làm sạch và tiền xử lý dữ liệu

  `04_machine_learning.ipynb`         Huấn luyện Logistic Regression và
                                      CatBoost

  `05_deep_learning.ipynb`            Xây dựng và huấn luyện mô hình MLP

  `06_model_evaluation.ipynb`         Đánh giá, so sánh mô hình và giải
                                      thích bằng SHAP
  -----------------------------------------------------------------------

## 4. Yêu cầu trước khi chạy

1.  Windows 10/11 (các lệnh bên dưới sử dụng PowerShell).
2.  Python 3.13.3 đã được cài đặt và có thể gọi bằng lệnh `python`.
3.  Visual Studio Code.
4.  Hai extension trong VS Code:
    -   Python (Microsoft)
    -   Jupyter (Microsoft)

Kiểm tra Python:

``` powershell
python --version
```

Kết quả mong đợi:

``` text
Python 3.13.3
```

## 5. Cài đặt và chạy dự án

### Bước 1: Mở dự án

Mở thư mục `Employee-Attrition-Prediction` bằng VS Code.

Mở Terminal trong VS Code: **Terminal → New Terminal**.

Đảm bảo Terminal đang ở thư mục gốc của dự án.

### Bước 2: Tạo môi trường ảo

Chỉ cần thực hiện lần đầu:

``` powershell
python -m venv .venv
```

### Bước 3: Kích hoạt môi trường ảo

``` powershell
.\.venv\Scripts\Activate.ps1
```

Khi kích hoạt thành công, đầu dòng Terminal sẽ có tiền tố `(.venv)`.

Nếu PowerShell chặn script, chạy lệnh dưới đây trong Terminal hiện tại
rồi kích hoạt lại:

``` powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### Bước 4: Cài đặt thư viện cơ bản

``` powershell
python -m pip install --upgrade pip
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter ipykernel
```

### Bước 5: Đăng ký Jupyter Kernel

``` powershell
python -m ipykernel install --user --name employee-attrition --display-name "Python (Employee Attrition)"
```

### Bước 6: Kiểm tra thư viện

``` powershell
python -c "import pandas, numpy, matplotlib, seaborn, sklearn; print('Environment OK')"
```

Nếu Terminal hiển thị `Environment OK`, các thư viện cơ bản đã được cài
và import thành công.

### Bước 7: Chọn Kernel trong VS Code

1.  Mở file `notebooks/01_data_collection.ipynb`.
2.  Nhấn **Select Kernel** ở góc trên bên phải.
3.  Chọn **Python (Employee Attrition)**.
4.  Có thể kiểm tra phiên bản Python ngay trong một cell:

``` python
import sys

print(sys.version)
```

Kết quả hiện tại của môi trường dự án là Python 3.13.3.

## 6. Chuẩn bị dataset

Dataset sử dụng: **IBM HR Analytics Employee Attrition**.

Nguồn Kaggle:

https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset

Thực hiện:

1.  Mở trang Kaggle và đăng nhập.
2.  Tải dataset về máy.
3.  Giải nén file ZIP.
4.  Đặt file CSV vào thư mục `dataset/`.
5.  Tên file dự kiến:

``` text
WA_Fn-UseC_-HR-Employee-Attrition.csv
```

Kiểm tra cấu trúc:

``` text
Employee-Attrition-Prediction/
└── dataset/
    └── WA_Fn-UseC_-HR-Employee-Attrition.csv
```

Không đưa file dữ liệu nhạy cảm hoặc thông tin cá nhân thật của nhân
viên vào repository công khai.

## 7. Chạy Notebook

Notebook được chạy theo thứ tự:

1.  `01_data_collection.ipynb`
2.  `02_data_exploration.ipynb`
3.  `03_data_preprocessing.ipynb`
4.  `04_machine_learning.ipynb`
5.  `05_deep_learning.ipynb`
6.  `06_model_evaluation.ipynb`

Trong mỗi Notebook:

1.  Chọn đúng Kernel `Python (Employee Attrition)`.
2.  Chạy từng cell bằng nút **Run Cell** hoặc `Shift + Enter`.
3.  Kiểm tra output và xử lý lỗi trước khi chạy cell tiếp theo.
4.  Lưu Notebook bằng `Ctrl + S`.

Không nên chạy các Notebook sau trước khi đã tạo và kiểm tra đầu ra cần
thiết từ các bước trước.

## 8. Kiểm tra nhanh môi trường

Chạy cell sau trong Notebook:

``` python
import sys
import pandas as pd
import numpy as np
import matplotlib
import seaborn as sns
import sklearn

print("Python:", sys.version)
print("Pandas:", pd.__version__)
print("NumPy:", np.__version__)
print("Matplotlib:", matplotlib.__version__)
print("Seaborn:", sns.__version__)
print("Scikit-learn:", sklearn.__version__)
print("Environment is ready!")
```

## 9. Xử lý lỗi thường gặp

### Không kích hoạt được `.venv`

Trong PowerShell:

``` powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

### VS Code không thấy Kernel

Kích hoạt `.venv`, sau đó chạy:

``` powershell
python -m pip install ipykernel
python -m ipykernel install --user --name employee-attrition --display-name "Python (Employee Attrition)"
```

Quay lại Notebook và chọn lại Kernel.

### Không tìm thấy file CSV

Kiểm tra: - File CSV đã nằm trong thư mục `dataset/` chưa. - Tên file có
đúng chính tả không. - Notebook đang chạy từ thư mục nào.

Có thể kiểm tra thư mục làm việc bằng:

``` python
from pathlib import Path

print("Current working directory:", Path.cwd())
print("Files in current directory:", list(Path.cwd().iterdir()))
```

### ImportError hoặc thiếu thư viện

Đảm bảo đã kích hoạt `.venv`, sau đó cài thư viện còn thiếu bằng:

``` powershell
python -m pip install ten-thu-vien
```

Thay `ten-thu-vien` bằng tên package cần cài.

## 10. Quy ước cập nhật README

**README.md là tài liệu hướng dẫn chạy dự án và phải được cập nhật cùng
với mỗi tính năng hoặc giai đoạn mới.**

Khi bổ sung tính năng, cần cập nhật các nội dung liên quan:

1.  Mô tả tính năng hoặc giai đoạn mới.
2.  Thư viện mới cần cài và lệnh cài đặt cụ thể.
3.  File hoặc Notebook được thêm/sửa.
4.  Cách cấu hình môi trường nếu có.
5.  Các lệnh hoặc thao tác để chạy tính năng.
6.  Đầu ra mong đợi và cách kiểm tra.
7.  Lỗi thường gặp và cách khắc phục nếu phát sinh.

Không ghi lệnh hoặc kết quả chưa được kiểm chứng như thể đã chạy thành
công. Nếu có thay đổi dependency, cần cập nhật hướng dẫn cài đặt tương
ứng và cân nhắc bổ sung `requirements.txt`.

## 11. Tiến độ hiện tại

-   [x] Xác định đề tài Employee Attrition Prediction.
-   [x] Tạo cấu trúc thư mục dự án.
-   [x] Xác nhận Python 3.13.3 chạy được trong Notebook.
-   [ ] Hoàn thành cài đặt môi trường và kiểm tra toàn bộ thư viện.
-   [ ] Giai đoạn 2: Đọc và kiểm tra dataset.
-   [ ] Giai đoạn 3: Khám phá dữ liệu (EDA).
-   [ ] Giai đoạn 4: Tiền xử lý dữ liệu.
-   [ ] Giai đoạn 5: Xây dựng Machine Learning.
-   [ ] Giai đoạn 6: Xây dựng Deep Learning MLP.
-   [ ] Giai đoạn 7: Đánh giá và giải thích mô hình.
-   [ ] Giai đoạn 8: Hoàn thiện báo cáo.

------------------------------------------------------------------------

**Quy tắc làm việc:** Mỗi khi dự án có tính năng, thư viện, Notebook
hoặc cách chạy mới, hãy cập nhật README.md để người khác có thể thiết
lập và chạy dự án theo tài liệu này.
