# P3.-Computer_Vision-Spatial_Domain_Filtering

Cải thiện hình ảnh qua Lọc miền không gian
(Image Enhancement Spatial Domain Filtering)
1. What is image filtering? (Lọc ảnh là gì? )
Lọc là quá trình thay thế một điểm ảnh bằng một giá trị dựa trên một số phép toán hoặc hàm số.
Các phép toán/hàm số sử dụng trên ảnh gốc được gọi là bộ lọc (filters).
hoặc masks, kernels, templates, windows...
Trong xử lý ảnh số, bộ lọc thường được sử dụng để:
Loại bỏ tần số cao trong ảnh: tức là làm mượt ảnh
Loại bỏ tần số thấp trong ảnh: tức là làm sắc nét hoặc phát hiện các cạnh trong ảnh


Spatial domain

Frequency domain



Point processing methods
Chuyển đổi một giá trị điểm ảnh đã cho thành một giá trị điểm ảnh mới dựa trên một số hàm số được xác định trước



Ví dụ:

Limitations of Point Operations
Chúng không biết gì về hàng xóm của chúng.
Hầu hết các đặc điểm của hình ảnh (đường viền - edges, kết cấu - textures, v.v.) liên quan đến một vùng lân cận không gian của các điểm ảnh.
Nếu chúng ta muốn cải thiện hoặc thao tác các đặc điểm này, chúng ta cần vượt ra ngoài các thao tác điểm.
What Point Operations Can’t Do
Blurring / Smoothing:


Sharpening:

Bộ lọc không gian - Spatial Filters
Các quy trình tổng quát có thể được ký hiệu bằng biểu thức: 
g(x, y) = T[ f (x, y)]
f(x,y) là hình ảnh đầu vào
g(x,y) là hình ảnh đã được xử lý
T là một toán tử trên f, được xác định trên một khu vực lân cận của (x,y)
sử dụng một khu vực hình ảnh con được đặt ở trung tâm tại (x,y)
hình dạng của khu vực lân cận (the neighborhood)
Hình tròn, hình vuông, hình chữ nhật

Khu vực lân cận 3×3 (3×3 neighborhood) quanh một điểm (x,y) trong một hình ảnh.


Operation
Các phép tính thông thường là các tổ hợp tuyến tính của giá trị pixel
Ví dụ: trọng số các giá trị pixel và cộng chúng lại với nhau.

Có thể thu được các kết quả khác nhau bằng cách sử dụng các trọng số khác nhau.
Ví dụ: làm mịn - smoothing, làm sắc nét - sharpening, phát hiện cạnh - edge detection.

Ví dụ: 
2. Correlation (Tương quan)
Một hình ảnh đã được lọc được tạo ra khi tâm của mặt nạ (center of the mask) đi qua từng pixel trong hình ảnh đầu vào.

Handling pixels close to boundaries

Geometric interpretation of correlation
Giả sử x và y là hai vector n chiều: x = (x1, x2, ..., xn) y = (y1, y2, ..., yn)
Tích vô hướng của x với y được định nghĩa là: x.y = x1y1 + x2y2+ ... + xnyn. sử dụng ký hiệu véc tơ: x.y = |x||y| cos(θ)
Sự tương quan tổng quát hóa khái niệm của tích vô hướng.
cos(θ) Đo lường độ tương đồng giữa x và y
x. y = |x||y| cos(θ) hoặc cos(θ) = (x.y) / (|x| |y|)
Tương quan chuẩn hóa - Normalized correlation (tức là, chia cho độ dài)

Normalized correlation
Đo lường sự tương đồng giữa các hình ảnh hoặc phần của hình ảnh.

Application example

3. Convolution (Tích chập)
Cũng giống như phép tương quan, ngoại trừ việc mặt nạ được lật lại, cả theo chiều ngang và chiều dọc.

Đối với các mặt nạ đối xứng (tức là, h(i,j)=h(-i,-j)), phép tích chập tương đương với phép tương quan! Ký hiệu: h * f = f * h

Convolution example



4. Smoothing linear filter (Bộ lọc làm mượt tuyến tính)
Linear spatial filtering
R = ω −1, −1 f(x-1,y-1) + ω −1,0 f(x-1,y) + … + ω 0,0 f(x,y) + ... + ω 1,0 f(x+1,y) + ω 1,1 f(x+1,y+1)
Lọc tuyến tính làm mịn (Smoothing Linear Filters): được biết đến như là bộ lọc trung bình hoặc bộ lọc thông thấp (averaging filter or lowpass filters).


Spatial Filters – smoothing, linear
Mean filters
Mean filters: 

Weighted average filters
ví dụ: 
biểu thức tổng quát: 


Spatial Filters – smoothing, nonlinear
Bộ lọc thống kê thứ tự (Order-statistic filters)
bộ lọc không gian phi tuyến tính
sắp xếp thứ tự/xếp hạng các pixel trong vùng ảnh mà bộ lọc bao gồm

5. Median filter (Bộ lọc trung vị)
Bộ lọc trung vị (Median filters)
thay thế giá trị của một pixel bằng giá trị trung vị của các pixel lân cận
ví dụ: Neighborhood values: 15, 19, 20, 23, 24, 25, 26, 27, 50 Median value: 24


khả năng giảm nhiễu xuất sắc (have excellent noise-reduction capabilities)


đặc biệt hiệu quả trong việc xử lý nhiễu muối và tiêu


Bộ lọc tối đa (Max filters)
giá trị lớn nhất của các pixel lân cận
hữu ích để tìm các điểm sáng nhất (brightest points) trong ảnh

Bộ lọc tối thiểu (Min filters)
giá trị nhỏ nhất của các pixel lân cận
hữu ích để tìm các điểm tối nhất (darkest points) trong ảnh
6. Sharpening (Làm sắc nét)
Mục tiêu chính
làm nổi bật chi tiết tinh xảo (highlight fine detail) trong ảnh
tăng cường chi tiết (enhance detail) đã bị mờ (blurred)

Làm sắc nét có thể được thực hiện bằng cách lấy đạo hàm không gian
Cho hàm một chiều f(x):
Đạo hàm bậc nhất: ∂f/∂x = f (x + 1) − f (x)
Đạo hàm bậc 2: ∂^2f/∂x^2 = = f (x + 1) + f (x − 1) − 2f(x)

Ví dụ: 
Toán tử / đạo hàm Laplace ( The Laplacian): đạo hàm bậc hai của một hàm hai chiều f(x,y): ∇^2f = ∂^2f/∂x^2 + ∂^2f/∂y^2 = = [f(x+1,y) + f(x-1,y)+f(x,y+1) + f(x,y-1)] – 4f(x,y)]
Sử dụng mặt nạ tích chập để xấp xỉ: 
Ví dụ đạo hàm Laplacian



Trong phần này chúng ta đã xem xét:
Các phép toán miền không gian - Spatial domain operations
Tích chập và tương quan - Convolution and correlation
Bộ lọc tuyến tính làm mịn - Smoothing linear filter
Bộ lọc trung vị - Median filter
Đạo hàm Laplace - The Laplacian


