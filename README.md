## Nội dung đồ án <a class="anchor" id="c1"></a>
Mục tiêu của đồ án là tìm hiểu các yếu tố quyết định mức lương và việc làm của các kỹ sư ngay sau khi tốt nghiệp. Các yếu tố như điểm số ở các cấp/trường đại học, kỹ năng của ứng viên, sự liên kết giữa trường đại học và các khu công nghiệp/công ty công nghệ, bằng cấp của sinh viên và điều kiện thị trường cho các ngành công nghiệp cụ thể sẽ ảnh hưởng đến điều này.

Bộ dữ liệu được sử dụng trong đồ án này thu thập tại Ấn Độ, nơi có hơn 6000 cơ sở đào tạo kỹ thuật công nghệ với khoảng 2,9 triệu sinh viên đang học tập. Mỗi năm, trung bình có 1,5 triệu sinh viên tốt nghiệp chuyên ngành Công nghệ/Kỹ thuật, tuy nhiên do thiếu kỹ năng cần thiết, ít hơn 20% trong số họ có việc làm phù hợp với chuyên môn của mình. Bộ dữ liệu này không chỉ giúp xây dựng công cụ dự đoán mức lương mà còn cung cấp thông tin về các yếu tố ảnh hưởng đến mức lương và chức danh công việc trên thị trường lao động. Sinh viên sẽ được khám phá những thông tin này trong phạm vi đồ án.

Chi tiết về dữ liệu tại: [Engineering Graduate Salary](https://www.kaggle.com/datasets/manishkc06/engineering-graduate-salary-prediction).
#### Dữ liệu sử dụng cho đồ án
Trong đồ án này, dữ liệu trên đã được thực hiện các bước tiền xử lý sau:
1. Loại bỏ các cột có giá trị là chuỗi: `DOB`, `10board`, `12board`, `Specialization`, `CollegeState`
5. Loại bỏ các cột liên quan đến định danh và năm: `ID`, `CollegeID`, `CollegeCityID`, `12graduation`, `GraduationYear`

Sau quá trình tiền xử lý, dữ liệu mới có:
- 2998 dòng dữ liệu
- 24 cột dữ liệu gồm:
    - 1 giá trị mục tiêu ($y$): `Salary`
    - 23 đặc trưng giải thích $(X)$ (đặc trưng giúp tìm giá trị mục tiêu) gồm: `Gender`, `10percentage`, `12percentage`, `CollegeTier`, `Degree`, `collegeGPA`, `CollegeCityTier`, `English`, `Logical`, `Quant`, `Domain`, `ComputerProgramming`, `ElectronicsAndSemicon`, `ComputerScience`, `MechanicalEngg`, `ElectricalEngg`, `TelecomEngg`, `CivilEngg`, `conscientiousness`, `agreeableness`, `extraversion`, `nueroticism`, `openess_to_experience`

Sinh viên được cung cấp 2 tập tin:
- `train.csv`: Chứa 2248 mẫu dùng để huấn luyện mô hình
- `test.csv`: Chứa 750 mẫu dùng để kiểm tra mô hình

Đoạn mã nguồn sau để thể hiện 5 mẫu dữ liệu đầu tiên trong tập `train.csv`.

##Trong đồ án này, yêu cầu thực hiện:

1. Xây dựng mô hình *dự đoán mức lương của kỹ sư* **sử dụng mô hình hồi quy tuyến tính**
- Yêu cầu 1a: Sử dụng 11 đặc trưng đầu tiên đề bài cung cấp bao gồm: `Gender`, `10percentage`, `12percentage`, `CollegeTier`, `Degree`, `collegeGPA`, `CollegeCityTier`, `English`, `Logical`, `Quant`, `Domain` (2 điểm)
	- Huấn luyện 1 lần duy nhất cho 11 đặc trưng nói trên cho toàn bộ tập huấn luyện (`train.csv`)
	- Thể hiện công thức cho mô hình hồi quy (tính $y$ theo 11 đặc trưng trên)
	- Báo cáo **1 kết quả trên tập kiểm tra (`test.csv`)** cho mô hình vừa huấn luyện được

- Yêu cầu 1b: Phân tích ảnh hưởng của **đặc trưng tính cách** dựa trên điểm các bài kiểm tra của AMCAT
	- Thử nghiệm lần lượt trên các đặc trưng tính cách gồm: `conscientiousness`, `agreeableness`, `extraversion`, `nueroticism`, `openess_to_experience`
    - Yêu cầu sử dụng **k-fold Cross Validation** (**k** tối thiểu là 5) để tìm ra đặc trưng tốt nhất trong các đặc trưng tính cách
	- Báo cáo **5 kết quả tương ứng cho 5 mô hình** từ k-fold Cross Validation (lấy trung bình)
	
	<center>

	| STT | Mô hình với 1 đặc trưng | MAE  |
	|:---:|:-----------------------:|:----:|
	|  1  | conscientiousness       |      |
	|  2  | agreeableness           |      |
	|  3  | extraversion            |      |
	|  4  | neuroticism             |      |
	|  5  | openness_to_experience  |      |

	</center>

	- Thể hiện công thức cho mô hình hồi quy theo đặc trưng tốt nhất (tính $y$ theo đặc trưng tốt nhất tìm được)
    - Báo cáo **1 kết quả trên tập kiểm tra (`test.csv`)** cho mô hình với đặc trưng tốt nhất tìm được

- Yêu cầu 1c: Phân tích ảnh hưởng của **đặc trưng ngoại ngữ, lô-gic, định lượng** đến mức lương của các kỹ sư dựa trên điểm các bài kiểm tra của AMCAT (1 điểm)

	- Thử nghiệm trên các đặc trưng gồm: `English`, `Logical`, `Quant`
    - Yêu cầu sử dụng **k-fold Cross Validation** (**k** tối thiểu là 5) để tìm ra đặc trưng tốt nhất
	- Báo cáo **3 kết quả tương ứng cho 3 mô hình** từ k-fold Cross Validation (lấy trung bình)
	
	<center>

	| STT | Mô hình với 1 đặc trưng | MAE  |
	|:---:|:-----------------------:|:----:|
	|  1  | English			        |      |
	|  2  | Logical		            |      |
	|  3  | Quant		            |      |

	</center>

	- Thể hiện công thức cho mô hình hồi quy theo đặc trưng tốt nhất (tính $y$ theo đặc trưng tốt nhất tìm được)
    - Báo cáo **1 kết quả trên tập kiểm tra (`test.csv`)** cho mô hình với đặc trưng tốt nhất tìm được
	
- Yêu cầu 1d: Xây dựng mô hình, tìm mô hình cho kết quả tốt nhất
	- Xây dựng `m` mô hình khác nhau (tối thiểu 3), đồng thời khác mô hình ở 1a, 1b và 1c
		- Mô hình có thể là sự kết hợp của 2 hoặc nhiều đặc trưng
		- Mô hình có thể sử dụng đặc trưng đã được chuẩn hóa hoặc biến đổi (bình phương, lập phương...)
		- Mô hình có thể sử dụng đặc trưng được tạo ra từ 2 hoặc nhiều đặc trưng khác nhau (cộng 2 đặc trưng, nhân 2 đặc trưng...)
		- ...
	- Gợi ý xây dựng mô hình:
		- Trực quan hóa các biến và đánh giá tính phân phối, tương quan giữa các biến, và xác định các đặc điểm đáng chú ý của dữ liệu
		- Phân tích mối quan hệ giữa biến mục tiêu và các biến dự đoán bằng các biểu đồ phân tán, ma trận tương quan, và biểu đồ histogram
		- $\to$ lựa chọn đặc trưng phù hợp cho mô hình mới

	- Yêu cầu **sử dụng phương pháp k-fold Cross Validation** (**k** tối thiểu là 5) để tìm ra mô hình tốt nhất trong `m` mô hình mà sinh viên xây dựng

	- Báo cáo **`m` kết quả tương ứng cho `m` mô hình** từ k-fold Cross Validation (lấy trung bình)

	<center>

	| STT |           Mô hình          | MAE  |
	|:---:|:--------------------------:|:----:|
	|  1  | Sử dụng 2 đặc trưng (a, b) |      |
	| ... | ...                        |      |
	|  m  | ...                        |      |

	</center>

	- Thể hiện công thức cho mô hình hồi quy tốt nhất mà sinh viên tìm được.
	- Báo cáo **1 kết quả trên tập kiểm tra (`test.csv`)** cho mô hình tốt nhất tìm được


- <ins>Lưu ý:</ins>
    - Kết quả báo cáo là độ đo MAE
	- Ở câu 1d, **mô hình sử dụng 2 đặc trưng** trên đặc trưng (a, b) và (b, c) cũng chỉ được tính là một mô hình sử dụng 2 đặc trưng
