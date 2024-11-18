
# Tài liệu thiết kế hệ thống "Payroll System"

---

## 1. Mô tả chung
Hệ thống "Payroll System" được thiết kế để quản lý quá trình xử lý lương và hỗ trợ các hoạt động liên quan như thanh toán ngân hàng, in phiếu lương, và quản lý thông tin về dự án. Dựa trên các phân tích ca sử dụng và các phần tử thiết kế, tài liệu này trình bày chi tiết các ca sử dụng, mô hình thiết kế, và lý do lựa chọn các thành phần.

---

## 2. Danh sách các ca sử dụng chính
Dựa trên phân tích hệ thống, các ca sử dụng chính bao gồm:

1. **Xử lý thanh toán trực tiếp qua ngân hàng**
   - **Miêu tả**: Xử lý việc thanh toán trực tiếp lương vào tài khoản ngân hàng của nhân viên.
   - **Thành phần chính**:
     - `PayrollController`: Điều phối quy trình xử lý lương.
     - `IBankSystem`: Giao tiếp với hệ thống ngân hàng để thực hiện thanh toán.
     - `BankSystem`: Subsystem thực hiện chi tiết việc thanh toán.

2. **In phiếu lương**
   - **Miêu tả**: In phiếu lương dưới dạng văn bản trên máy in được chỉ định.
   - **Thành phần chính**:
     - `PayrollController`: Điều phối việc xử lý in phiếu lương.
     - `IPrintService`: Giao tiếp với máy in.
     - `PrintService`: Subsystem quản lý việc in phiếu.

3. **Quản lý thông tin dự án**
   - **Miêu tả**: Truy vấn các thông tin liên quan đến mã dự án và cập nhật thông tin thẻ thời gian của nhân viên.
   - **Thành phần chính**:
     - `TimecardController`: Điều phối các thao tác trên thông tin thẻ thời gian.
     - `IProjectManagementDatabase`: Giao tiếp với cơ sở dữ liệu dự án.
     - `ProjectManagementDatabase`: Subsystem quản lý thông tin dự án.
---

## 3. Mô hình chi tiết

### 3.1 Subsystem Context Diagram

#### 1. **BankSystem Subsystem**
   - **Miêu tả**:
     Hệ thống thực hiện việc giao tiếp với ngân hàng để xử lý các giao dịch thanh toán lương.
   - **Các thành phần liên quan**:
     - `PayrollController`: Điều phối xử lý lương.
     - `IBankSystem`: Interface đại diện giao tiếp với ngân hàng.
     - `Paycheck`, `BankInformation`: Các đối tượng chính.

---

#### 2. **PrintService Subsystem**
   - **Miêu tả**:
     Hệ thống hỗ trợ in các phiếu lương cho nhân viên.
   - **Các thành phần liên quan**:
     - `PayrollController`: Điều phối việc xử lý in phiếu lương.
     - `IPrintService`: Interface đại diện giao tiếp với máy in.
     - `Paycheck`: Thông tin lương của nhân viên.
---

#### 3. **ProjectManagementDatabase Subsystem**
   - **Miêu tả**:
     Hệ thống quản lý dữ liệu liên quan đến dự án và mã dự án.
   - **Các thành phần liên quan**:
     - `TimecardController`: Điều phối xử lý dữ liệu thẻ thời gian.
     - `IProjectManagementDatabase`: Interface giao tiếp cơ sở dữ liệu dự án.
     - `ChargeNumList`: Danh sách mã dự án.
---

## 4. Giải thích thiết kế

1. **Tính phân lớp (Layered Architecture)**
   - **Lý do**: Thiết kế sử dụng kiến trúc phân lớp giúp tách biệt các trách nhiệm của hệ thống (Application, Business Services, Middleware) để dễ dàng bảo trì và mở rộng.
   - **Ví dụ**: Các giao tiếp với hệ thống ngân hàng và máy in được đặt trong lớp *Business Services*, tách biệt với lớp *Application* xử lý logic nghiệp vụ.

2. **Sử dụng Interface để giao tiếp**
   - **Lý do**: Các Interface (`IBankSystem`, `IPrintService`, `IProjectManagementDatabase`) đảm bảo sự linh hoạt trong việc thay thế hoặc tích hợp với các hệ thống khác.
   - **Ví dụ**: Interface `IBankSystem` cho phép thay đổi hệ thống ngân hàng mà không ảnh hưởng đến các thành phần khác.

3. **Quản lý subsystem qua proxy**
   - **Lý do**: Sử dụng các proxy subsystem giúp ẩn đi chi tiết triển khai, chỉ để lộ các phương thức cần thiết. Điều này giảm độ phức tạp và tăng tính bảo mật.
   - **Ví dụ**: Proxy của `BankSystem` thực hiện xử lý các giao dịch mà không cần tiết lộ chi tiết triển khai cho lớp trên.

4. **Tách biệt thành phần nghiệp vụ và giao diện**
   - **Lý do**: Việc tách biệt các thành phần như `PayrollController` và `GUI Framework` giúp tăng tính linh hoạt trong việc thay đổi giao diện người dùng mà không ảnh hưởng đến logic nghiệp vụ.

---

## 5. Kết luận
Thiết kế hệ thống "Payroll System" tập trung vào tính linh hoạt, khả năng mở rộng và dễ bảo trì. Các ca sử dụng được cụ thể hóa qua việc phân tích và chi tiết hóa thành các subsystem với các interface rõ ràng, đảm bảo hệ thống hoạt động hiệu quả trong môi trường doanh nghiệp phức tạp.

