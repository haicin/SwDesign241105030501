# Lab 2: Phân Tích và Mô Phỏng Hệ Thống Payroll System


# Lab 02: Phân tích Ca sử dụng (Use Cases)

## 1. **Maintain Timecard** (Cập nhật thông tin chấm công)
- **Mô tả:** Quá trình nhân viên hoặc quản lý nhập thông tin chấm công (timecard) vào hệ thống để ghi nhận giờ làm việc và các chi tiết liên quan. Thông tin này sẽ được dùng để tính lương sau này.
- **Actor:** Nhân viên, Quản lý
- **Các bước thực hiện:**
  1. **Đăng nhập vào hệ thống**: Nhân viên hoặc quản lý cần đăng nhập vào hệ thống với tài khoản hợp lệ.
  2. **Chọn chức năng "Maintain Timecard"**: Người dùng chọn chức năng để cập nhật thông tin chấm công.
  3. **Nhập thông tin chấm công**: Nhân viên nhập các thông tin cần thiết như ngày làm việc, số giờ làm, và mã nhân viên.
  4. **Lưu thông tin vào hệ thống**: Sau khi nhập xong, thông tin chấm công được lưu vào cơ sở dữ liệu.
  5. **Thông báo thành công**: Hệ thống sẽ thông báo việc cập nhật thông tin thành công.
- **Ngoại lệ:**
  - **Dữ liệu không hợp lệ:** Số giờ làm việc vượt quá giới hạn, ngày làm việc không hợp lệ, hoặc mã nhân viên không tồn tại.
  - **Không đủ quyền truy cập:** Người dùng không có quyền nhập hoặc chỉnh sửa thông tin chấm công.
  - **Lỗi hệ thống:** Lỗi khi lưu dữ liệu vào cơ sở dữ liệu.

## 2. **Calculate Payroll** (Tính toán bảng lương)
- **Mô tả:** Hệ thống tính toán bảng lương cho nhân viên dựa trên thông tin chấm công và các yếu tố khác như bảng lương cơ bản, các khoản khấu trừ (bảo hiểm, thuế).
- **Actor:** Hệ thống, Quản lý
- **Các bước thực hiện:**
  1. **Truy xuất dữ liệu chấm công:** Hệ thống lấy dữ liệu từ thông tin chấm công của nhân viên.
  2. **Tính toán thu nhập:** Hệ thống tính toán tổng thu nhập dựa trên số giờ làm và mức lương cơ bản, bao gồm các khoản làm thêm nếu có.
  3. **Trừ các khoản khấu trừ:** Các khoản bảo hiểm, thuế và các khoản trừ khác được tính toán và trừ từ tổng thu nhập.
  4. **Cập nhật bảng lương:** Hệ thống hiển thị bảng lương cho quản lý sau khi tính toán xong.
- **Ngoại lệ:**
  - **Dữ liệu chấm công không hợp lệ:** Nếu dữ liệu chấm công sai hoặc thiếu, hệ thống không thể tính toán lương.
  - **Lỗi tính toán:** Nếu thông tin về lương cơ bản hoặc công thức tính bị sai, bảng lương sẽ không chính xác.
  - **Không đủ quyền truy cập:** Quản lý không thể tính lương nếu không có quyền hạn phù hợp.

## 3. **Select Payment Method** (Chọn phương thức thanh toán lương)
- **Mô tả:** Nhân viên lựa chọn phương thức nhận lương (chuyển khoản ngân hàng, tiền mặt, v.v.) để hệ thống ghi nhận và thực hiện thanh toán khi đến kỳ trả lương.
- **Actor:** Nhân viên
- **Các bước thực hiện:**
  1. **Đăng nhập vào hệ thống:** Nhân viên đăng nhập vào tài khoản cá nhân của mình.
  2. **Chọn "Select Payment Method":** Nhân viên chọn chức năng thay đổi phương thức thanh toán.
  3. **Lựa chọn phương thức thanh toán:** Nhân viên chọn phương thức thanh toán mong muốn (chuyển khoản ngân hàng, tiền mặt, v.v.).
  4. **Lưu thông tin lựa chọn:** Hệ thống ghi lại phương thức thanh toán đã chọn.
- **Ngoại lệ:**
  - **Phương thức thanh toán không hợp lệ:** Nếu phương thức thanh toán không hợp lệ hoặc không được hỗ trợ.
  - **Không có quyền thay đổi:** Nhân viên không có quyền thay đổi phương thức thanh toán nếu chính sách công ty không cho phép.

## 4. **View Pay Statement** (Xem bảng lương)
- **Mô tả:** Nhân viên có thể xem bảng lương của mình qua hệ thống để kiểm tra các khoản thu nhập và khấu trừ.
- **Actor:** Nhân viên
- **Các bước thực hiện:**
  1. **Đăng nhập vào hệ thống:** Nhân viên sử dụng tài khoản của mình để đăng nhập.
  2. **Chọn "View Pay Statement":** Nhân viên chọn chức năng để xem bảng lương của mình.
  3. **Xem bảng lương:** Hệ thống hiển thị bảng lương cho nhân viên.
- **Ngoại lệ:**
  - **Không có bảng lương:** Nếu bảng lương chưa được tính hoặc chưa được cập nhật.
  - **Không đủ quyền truy cập:** Nhân viên không có quyền xem bảng lương nếu quyền truy cập của họ bị hạn chế.
  - **Lỗi hiển thị:** Lỗi phần mềm hoặc kết nối khiến bảng lương không thể hiển thị.

## Tổng kết
Các ca sử dụng trên mô tả quy trình quản lý thời gian làm việc, tính toán lương và quản lý phương thức thanh toán cho nhân viên trong một hệ thống quản lý nhân sự. Hệ thống cần đảm bảo tính chính xác của dữ liệu đầu vào và quyền truy cập hợp lý để tránh các lỗi và sự cố trong quá trình thực hiện.



### 3.3 Mã Java Mô Phỏng Ca Sử Dụng **Maintain Timecard**

```java
import java.util.ArrayList;
import java.util.List;


class Timecard {
    private String employeeId;
    private List<TimeEntry> entries;

    public Timecard(String employeeId) {
        this.employeeId = employeeId;
        this.entries = new ArrayList<>();
    }

    public String getEmployeeId() {
        return employeeId;
    }


    public void addTimeEntry(TimeEntry entry) {
        entries.add(entry);
    }


    public int calculateTotalHours() {
        int totalHours = 0;
        for (TimeEntry entry : entries) {
            totalHours += entry.getHours();
        }
        return totalHours;
    }

    public List<TimeEntry> getEntries() {
        return entries;
    }
}


class TimeEntry {
    private String date;
    private int hours;

    public TimeEntry(String date, int hours) {
        this.date = date;
        this.hours = hours;
    }

    public String getDate() {
        return date;
    }

    public int getHours() {
        return hours;
    }
}


class TimecardManager {
    private List<Timecard> timecards;

    public TimecardManager() {
        this.timecards = new ArrayList<>();
    }


    public void submitTimecard(Timecard timecard, List<TimecardRule> rules) {
        System.out.println("Submitting timecard for employee: " + timecard.getEmployeeId());
        // Kiểm tra tính hợp lệ của thẻ giờ làm việc
        boolean isValid = true;
        for (TimecardRule rule : rules) {
            if (!rule.validate(timecard)) {
                isValid = false;
                break;
            }
        }


        if (isValid) {
            approveTimecard(timecard);
        } else {
            rejectTimecard(timecard);
        }
    }


    private void approveTimecard(Timecard timecard) {
        System.out.println("Timecard for employee " + timecard.getEmployeeId() + " has been approved.");
    }

    private void rejectTimecard(Timecard timecard) {
        System.out.println("Timecard for employee " + timecard.getEmployeeId() + " has been rejected.");
    }
}


interface TimecardRule {
    boolean validate(Timecard timecard);
}

class MaxHoursRule implements TimecardRule {
    private int maxHours;

    public MaxHoursRule(int maxHours) {
        this.maxHours = maxHours;
    }

    @Override
    public boolean validate(Timecard timecard) {
        return timecard.calculateTotalHours() <= maxHours;
    }
}

class Employee {
    private String id;
    private Timecard timecard;

    public Employee(String id) {
        this.id = id;
        this.timecard = new Timecard(id);
    }

    public String getId() {
        return id;
    }

    public Timecard getTimecard() {
        return timecard;
    }


    public void addTimeEntry(String date, int hours) {
        TimeEntry entry = new TimeEntry(date, hours);
        timecard.addTimeEntry(entry);
    }


    public void submitTimecard(TimecardManager manager, List<TimecardRule> rules) {
        manager.submitTimecard(timecard, rules);
    }
}


public class Main {
    public static void main(String[] args) {

        Employee employee = new Employee("E123");
        employee.addTimeEntry("2024-11-01", 8);
        employee.addTimeEntry("2024-11-02", 9);

        List<TimecardRule> rules = new ArrayList<>();
        rules.add(new MaxHoursRule(15));  

        TimecardManager manager = new TimecardManager();
        employee.submitTimecard(manager, rules);
    }
}

