### 1. Phân tích kiến trúc
**2. a. Đề xuất kiến trúc**:

**Kiến trúc 3-tầng (Three-Tier Architecture) được đề xuất cho hệ thống quản lý bảng lương vì lý do sau**:

- **Tầng giao diện (Presentation Layer)**: Cung cấp giao diện người dùng, cho phép nhân viên nhập thẻ chấm công, chọn phương thức thanh toán và tạo báo cáo. Ứng dụng desktop Windows-based sẽ chạy trên máy tính cá nhân của nhân viên toàn công ty.

- **Tầng logic nghiệp vụ (Business Logic Layer)**: Tầng này xử lý các quy tắc nghiệp vụ như tính toán lương, quản lý hoa hồng, kiểm tra số giờ làm việc, và cập nhật thông tin nhân viên. Nó đóng vai trò trung gian giữa giao diện người dùng và tầng cơ sở dữ liệu, bảo đảm tính bảo mật và đúng logic.

- **Tầng cơ sở dữ liệu (Database Layer)**: Lưu trữ thông tin nhân viên, thẻ chấm công, lệnh mua hàng, và các thông tin về dự án (trong cơ sở dữ liệu legacy DB2). Tầng này cho phép truy cập dữ liệu mà không thay đổi cấu trúc hệ thống hiện có.
  ![Diagram](https://www.planttext.com/api/plantuml/png/T5FDJW8n4BxtAIedFV0270mWn9204i476Di16xlRJJjBiZ4ycGSVoLUmArreozfZPxw_cVRdwtli22pLXMOt4dUgHFuoVzXEdXwNSouqECTO1U83ziW7QuiEIm9IfkHBQD0E-2VZ_bmmhmxjeYIqEn0OggSZbQiqDFEYqgP1d261qkxsBch15hXL1GgmSb7kJ59rg57G6fh2zwsGteqCzICxHZQdjVCvdEDBirVYFwEUnngjDsWFAdDQMICyFdGa7WHeKMiWt806svprK-ukumfAxwYrc_23b5r7GbvNqZDtfIX_ccy617mYn5_4_d3d8K-U4-KzKbUQDWkPZXSEcDdASuM9vAmjijjQGkdbEeZt78T9dybmU9_lOyHT_LOeYdYlCJrp7eKfNfuNovWZiJQ85o9ZaLUdA-x1m7g8Oxs0yx4vXYkk_BfwjNfDMYIhy90lUuobRF_YBm000F__0m00)
  
### b. Lý do lựa chọn:
  
 - Tách biệt rõ ràng giữa giao diện người dùng, logic nghiệp vụ, và dữ liệu, giúp hệ thống dễ bảo trì, nâng cấp và mở rộng.

- Bảo mật: Phân chia vai trò truy cập dữ liệu một cách rõ ràng giữa các tầng giúp bảo vệ dữ liệu nhạy cảm như thông tin lương bổng.

- ## Tương thích với hệ thống cũ: Cho phép hệ thống mới kết nối với cơ sở dữ liệu cũ (DB2) mà không cần thay đổi cấu trúc hiện tại.

### 2. Cơ chế phân tích
**Cơ chế cần giải quyết trong bài toán**:
### - Cơ chế tính lương:

- Tự động tính toán lương cho nhân viên dựa trên loại nhân viên (theo giờ, cố định, hoa hồng) và số giờ làm việc trong timecard.
Tính toán tăng lương khi làm thêm giờ (> 8 giờ/ngày với nhân viên theo giờ).

### Cơ chế quản lý hoa hồng:

- Tính hoa hồng dựa trên lệnh mua hàng của nhân viên bán hàng.

- Hệ thống tự động tổng hợp hoa hồng dựa trên mức % được cấu hình cho từng nhân viên.
Cơ chế bảo mật và phân quyền:

- Đảm bảo chỉ có nhân viên được truy cập và chỉnh sửa thông tin cá nhân (timecard, phương thức thanh toán).
- Quản trị viên lương có quyền thêm, xóa, sửa thông tin nhân viên và xem các báo cáo.
### Cơ chế xử lý timecard:

- Cho phép nhân viên nhập số giờ làm việc, kiểm tra tính hợp lệ của dữ liệu, và lưu thông tin timecard để tính lương.
### Cơ chế chọn phương thức thanh toán:

- Nhân viên có thể chọn cách nhận lương (chuyển khoản, nhận trực tiếp, hoặc gửi qua bưu điện), và hệ thống sẽ lưu lại thông tin để xử lý trong các kỳ lương tiếp theo.
### 3. Phân tích ca sử dụng: Select Payment
### a. Các lớp phân tích cho ca sử dụng Select Payment:
- **Employee (Nhân viên)**: Tương tác với hệ thống để chọn phương thức thanh toán.
- **PaymentMethod (Phương thức thanh toán)**: Lưu trữ thông tin về các phương thức thanh toán (chuyển khoản, nhận tại văn phòng, gửi qua bưu điện).
- **PayrollSystem (Hệ thống lương)**: Quản lý việc lưu trữ và cập nhật phương thức thanh toán của nhân viên.
- **BankSystem (Hệ thống ngân hàng)**: Nếu chọn chuyển khoản, hệ thống sẽ liên kết với ngân hàng để thiết lập phương thức thanh toán.
### Cơ chế báo cáo:

- Cung cấp cho nhân viên khả năng tạo báo cáo về tổng số giờ làm việc, lương đã nhận, số ngày nghỉ còn lại, và tổng số giờ làm việc trên các dự án.
- # 4. Phân tích ca sử dụng Maintain Timecard

## Biểu đồ lớp phân tích cho ca sử dụng Maintain Timecard

## Hình ảnh UML

![Diagram](https://www.planttext.com/api/plantuml/png/d9DDReCm48Ntd6B4YbG1ALk4K1QDr4hDfie59k0GLyP6zX0rQdkoBdgaNg76_9GGL4NT83FpvfldiVtz-RKsX9hgKdYPG6DWKrP2dHc3DmyW1DRzFkOnS4ak9h5aCHZIN1Os063gVSbfnqkMeSu3wXOnzA65z-5r_3xKyNljc3_NqxcyHxADcs-ha_aaGefGFAXQcnWEGY4vUvZdJTUD97qEyg5Y2SUHSk6a6Ogi5ZQv6qZ1ZFajIYoOdkp1efwueQHNfRSEnvciAgrEx4hN3Q4LQVR2icjMfrdQF1eb-xEPCVvSY_PaayGMC7t0ZAMjpnCAtWpdBwSnx9KI3EKlUOklRam3-H-awLZzbGzX6ARWt_b3oMsgnePtuIcAtjFBz7357K7puaWDPHL5utPhUxtii_W1003__mC0)

### Giải thích:
- **Employee**: 
  - Đại diện cho một nhân viên, có các thuộc tính như ID nhân viên và tên. 
  - Nhân viên có thể gửi thẻ giờ làm việc bằng cách gọi phương thức `submitTimecard`.
  
- **Timecard**: 
  - Đại diện cho một thẻ giờ làm việc, có các thuộc tính như ID thẻ giờ, ID nhân viên, ngày bắt đầu, ngày kết thúc và tổng số giờ làm việc. 
  - Thẻ giờ có thể thêm mục nhập giờ làm việc và tính toán tổng số giờ làm việc.
  
- **TimecardManager**: 
  - Quản lý các thẻ giờ làm việc, bao gồm gửi, phê duyệt và từ chối thẻ giờ làm việc. 
  - Nó cũng quản lý các quy tắc kiểm tra thẻ giờ làm việc.
  
- **TimecardRule**: 
  - Là một **interface** định nghĩa phương thức `validateTimecard` để kiểm tra tính hợp lệ của thẻ giờ làm việc.
  
- **MaxHoursRule**: 
  - Là một lớp cụ thể triển khai interface `TimecardRule`, kiểm tra xem tổng số giờ làm việc trong thẻ giờ có vượt quá giới hạn tối đa hay không.

## Biểu đồ sequence mô tả hành vi của ca sử dụng Maintain Timecard

## Hình ảnh UML

![Diagram](https://www.planttext.com/api/plantuml/png/Z58xRWCX4EqvnPHhoRx0IexSM8gBD8ulC859GZGB20PBFbiA7ybN24XBVekYT33lo-VsVjqbmIXvOeLQV8Jz5DXVY5GeOwjjG2TmiXDfZEO17RvGx6BTuJ4pATKyONFtYOo0njJDtacy30Q5rl3gSqmhrJW_-HfPPowyanVa-qeTLbtlkUO8AJzDLjfua7dnbJ0plujhvH7EoBPs-aDRYR3fnSvYwzsHKcPH2baMKzXkGM8c1RyTkcV14A8_BmiTIYNYH5t_Pop8FmCYlP5UNjR1h0k4oRkIuunQtbqnQwymGfCz2afEQbSavNDz0000__y30000)
### Giải thích:
1. Nhân viên thêm mục nhập giờ làm việc vào thẻ giờ bằng cách gọi phương thức `addTimeEntry` trên đối tượng `Timecard`.
2. `Timecard` tính toán tổng số giờ làm việc bằng cách gọi phương thức `calculateTotalHours`.
3. Nhân viên gửi thẻ giờ làm việc bằng cách gọi phương thức `submitTimecard` trên `TimecardManager`.
4. `TimecardManager` kiểm tra tính hợp lệ của thẻ giờ làm việc bằng cách gọi phương thức `validateTimecard` trên các đối tượng `TimecardRule`.
5. `TimecardRule` trả về kết quả kiểm tra tính hợp lệ cho `TimecardManager`.
6. Nếu thẻ giờ làm việc hợp lệ, `TimecardManager` phê duyệt thẻ giờ bằng cách gọi phương thức `approveTimecard`. Nếu không hợp lệ, `TimecardManager` từ chối thẻ giờ bằng cách gọi phương thức `rejectTimecard` với lý do từ chối.
7. `TimecardManager` trả về trạng thái của thẻ giờ làm việc (được phê duyệt hoặc bị từ chối) cho nhân viên.

# 5. Hợp nhất kết quả phân tích

## Hình ảnh UML

![Diagram](https://www.planttext.com/api/plantuml/png/f5HBRi8m4Dtd51QhW02fsmX5LJzIAnK9LLnWI0P8wzZ8dg2YjYVheaVg5UeuJXe7g6ZPHF7Cc-StusT_VNnUQW95HSw3X8FMx3RVSBb3PAy1OoE6RdcVHYmJP6C2SeoO9fM9bGriO9UZe2dIMXhShBqq0COqSap8YuU_5VMhgcAHPpJFSan0fI6vduZLeNxm7ZZPTSZ9hh5jsOTQiStV09b-oc-54sadGfA0tyb2wOWjkGIoyY1Dorrl1QbTc3OLGxPk8QjE4k19mKrotZ25BV5UxxQ3oSGeHBM41EFOKcoKJ51h1mqXbuKWjycmwIrgpgz5VmrwxUei-LbaLo2Uvmg4Ng8wdytLp2e6gTpnUTumetp8D4syALL3KRWo6LH_TTOPYckZJK702bN7RxNM6XMVQcHhg8tHjSKzd3DitxNyPAxICSpGv45BKL_F0y8V2uv7FBO5dfL6_arfn1PISWJnmpo55slfXlaVJCspqxleiP7ALciQnNRXloR7SEFneDTG1tksikXHYHnq6TktOpn-Ypjfp-y7ybq_U3irWav2bVCBl67Q_RpqfNcTp6Fz3G00__y30000)

## Mô tả:

- **Lớp Employee**:
  - Đại diện cho một nhân viên trong hệ thống.
  - Có các thuộc tính như ID nhân viên, tên và phương thức thanh toán.
  - Có phương thức để chọn phương thức thanh toán và gửi thẻ giờ làm việc.

- **Lớp Timecard**:
  - Đại diện cho một thẻ giờ làm việc.
  - Có các thuộc tính như ID thẻ giờ, ID nhân viên, ngày bắt đầu, ngày kết thúc và tổng số giờ làm việc.
  - Có phương thức để thêm mục nhập giờ làm việc và tính toán tổng số giờ làm việc.

- **Lớp PaymentMethod**:
  - Là một **interface** định nghĩa phương thức xử lý thanh toán.
  - Có phương thức `processPayment` để xử lý thanh toán với số tiền và thông tin nhân viên.

- **Lớp CashPayment và BankTransfer**:
  - Là các lớp cụ thể triển khai interface `PaymentMethod`.
  - Tương ứng với các phương thức thanh toán bằng tiền mặt và chuyển khoản ngân hàng.

- **Lớp PaymentProcessor**:
  - Quản lý các phương thức thanh toán đã đăng ký.
  - Có phương thức để đăng ký phương thức thanh toán và xử lý thanh toán cho nhân viên với số tiền nhất định.

- **Lớp TimecardManager**:
  - Quản lý các thẻ giờ làm việc và các quy tắc kiểm tra thẻ giờ.
  - Có phương thức để gửi, phê duyệt và từ chối thẻ giờ làm việc.

- **Lớp TimecardRule**:
  - Là một **interface** định nghĩa phương thức kiểm tra tính hợp lệ của thẻ giờ làm việc.

- **Lớp MaxHoursRule**:
  - Là một lớp cụ thể triển khai interface `TimecardRule`.
  - Kiểm tra xem tổng số giờ làm việc trong thẻ giờ có vượt quá giới hạn tối đa hay không.

Trong mô hình hợp nhất này, các lớp phân tích từ cả hai ca sử dụng đã được kết hợp lại. Lớp `Employee` liên kết với cả `PaymentMethod` và `Timecard`. Các lớp `PaymentProcessor` và `TimecardManager` tương ứng với xử lý thanh toán và quản lý thẻ giờ làm việc. Các quy tắc kiểm tra được áp dụng cho thẻ giờ làm việc thông qua lớp `TimecardRule`.

Mô hình này cung cấp một cái nhìn tổng quan về các lớp và mối quan hệ giữa chúng trong hệ thống quản lý nhân viên, thanh toán và thẻ giờ làm việc. Nó có thể được sử dụng làm cơ sở cho việc thiết kế và triển khai hệ thống trong các giai đoạn tiếp theo.

