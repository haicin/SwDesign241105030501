# Lab 2: Phân Tích và Mô Phỏng Hệ Thống Payroll System

## 1. Giới thiệu

Hệ thống Payroll System được xây dựng nhằm quản lý bảng lương cho nhân viên trong công ty. Hệ thống cho phép tính toán lương, theo dõi giờ làm việc của nhân viên, quản lý hoa hồng và các phương thức thanh toán khác nhau. Trong bài lab này, chúng ta sẽ thực hiện phân tích các ca sử dụng trong hệ thống và viết mã Java mô phỏng ca sử dụng **Maintain Timecard**.

## 2. Phân Tích Kiến Trúc Hệ Thống

### 2.1 Kiến Trúc 3 Tầng

Hệ thống Payroll sử dụng kiến trúc **3 tầng** để tách biệt rõ ràng giữa giao diện người dùng, logic nghiệp vụ và cơ sở dữ liệu.

- **Tầng giao diện (Presentation Layer)**: Giao diện người dùng cho phép nhân viên nhập thẻ chấm công, chọn phương thức thanh toán và tạo báo cáo.
- **Tầng logic nghiệp vụ (Business Logic Layer)**: Tầng này xử lý các quy tắc nghiệp vụ như tính toán lương, quản lý hoa hồng, kiểm tra số giờ làm việc và cập nhật thông tin nhân viên.
- **Tầng cơ sở dữ liệu (Database Layer)**: Lưu trữ thông tin nhân viên, thẻ chấm công, và các thông tin liên quan đến các dự án và lệnh mua hàng.

### 2.2 Các Ca Sử Dụng Chính

1. **Maintain Timecard**: Nhân viên thêm và quản lý thẻ chấm công.
2. **Select Payment Method**: Nhân viên chọn phương thức thanh toán.
3. **Calculate Payroll**: Tính toán bảng lương dựa trên số giờ làm việc và các yếu tố khác.
4. **Generate Report**: Tạo các báo cáo lương cho nhân viên.
5. **Administer Employee Information**: Quản lý thông tin nhân viên, bao gồm thêm, sửa, xóa thông tin nhân viên.
6. **Manage Commission**: Quản lý hoa hồng cho nhân viên bán hàng.

## 3. Phân Tích Ca Sử Dụng **Maintain Timecard**

### 3.1 Mô Tả Ca Sử Dụng **Maintain Timecard**

Ca sử dụng **Maintain Timecard** cho phép nhân viên nhập số giờ làm việc vào thẻ chấm công. Sau đó, hệ thống sẽ kiểm tra tính hợp lệ của thẻ giờ, ví dụ như kiểm tra số giờ làm việc có vượt quá giới hạn hay không. Nếu hợp lệ, thẻ giờ sẽ được gửi đi để phê duyệt.

- **Nhân viên** nhập giờ làm việc vào thẻ chấm công.
- **Thẻ giờ** sẽ được tính toán tổng số giờ.
- **TimecardManager** sẽ kiểm tra tính hợp lệ của thẻ giờ làm việc theo các quy tắc đã định sẵn (ví dụ: giờ làm việc không được vượt quá giới hạn tối đa).
- Nếu thẻ giờ hợp lệ, nó sẽ được phê duyệt, ngược lại sẽ bị từ chối.

### 3.2 Các Lớp Cần Thiết

- **Employee**: Đại diện cho nhân viên và quản lý thẻ chấm công của họ.
- **Timecard**: Đại diện cho thẻ giờ làm việc của nhân viên.
- **TimecardManager**: Quản lý việc gửi, phê duyệt và từ chối thẻ giờ làm việc.
- **TimecardRule**: Quy tắc kiểm tra tính hợp lệ của thẻ giờ làm việc.
- **MaxHoursRule**: Quy tắc giới hạn số giờ làm việc tối đa.

### 3.3 Mã Java Mô Phỏng Ca Sử Dụng **Maintain Timecard**

```java
import java.util.ArrayList;
import java.util.List;

// Lớp Timecard đại diện cho một thẻ giờ làm việc của nhân viên
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

    // Thêm một mục nhập giờ làm việc
    public void addTimeEntry(TimeEntry entry) {
        entries.add(entry);
    }

    // Tính tổng số giờ làm việc trong thẻ giờ
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

// Lớp TimeEntry đại diện cho một mục nhập giờ làm việc
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

// Lớp TimecardManager chịu trách nhiệm quản lý các thẻ giờ làm việc
class TimecardManager {
    private List<Timecard> timecards;

    public TimecardManager() {
        this.timecards = new ArrayList<>();
    }

    // Gửi thẻ giờ làm việc cho phê duyệt
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

        // Nếu thẻ hợp lệ, phê duyệt thẻ giờ
        if (isValid) {
            approveTimecard(timecard);
        } else {
            rejectTimecard(timecard);
        }
    }

    // Phê duyệt thẻ giờ
    private void approveTimecard(Timecard timecard) {
        System.out.println("Timecard for employee " + timecard.getEmployeeId() + " has been approved.");
    }

    // Từ chối thẻ giờ
    private void rejectTimecard(Timecard timecard) {
        System.out.println("Timecard for employee " + timecard.getEmployeeId() + " has been rejected.");
    }
}

// Interface TimecardRule định nghĩa các quy tắc kiểm tra thẻ giờ
interface TimecardRule {
    boolean validate(Timecard timecard);
}

// Lớp MaxHoursRule kiểm tra tổng số giờ làm việc có vượt quá giới hạn tối đa không
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

// Lớp Employee đại diện cho nhân viên
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

    // Thêm mục nhập giờ làm việc vào thẻ giờ
    public void addTimeEntry(String date, int hours) {
        TimeEntry entry = new TimeEntry(date, hours);
        timecard.addTimeEntry(entry);
    }

    // Gửi thẻ giờ làm việc để phê duyệt
    public void submitTimecard(TimecardManager manager, List<TimecardRule> rules) {
        manager.submitTimecard(timecard, rules);
    }
}

// Demo chạy thử hệ thống
public class Main {
    public static void main(String[] args) {
        // Tạo nhân viên và thêm giờ làm việc
        Employee employee = new Employee("E123");
        employee.addTimeEntry("2024-11-01", 8);
        employee.addTimeEntry("2024-11-02", 9);

        // Tạo các quy tắc kiểm tra
        List<TimecardRule> rules = new ArrayList<>();
        rules.add(new MaxHoursRule(15));  // Giới hạn số giờ làm việc tối đa trong tuần là 15 giờ

        // Tạo TimecardManager để quản lý thẻ giờ
        TimecardManager manager = new TimecardManager();
        
        // Nhân viên gửi thẻ giờ làm việc cho phê duyệt
        employee.submitTimecard(manager, rules);
    }
}

