# Bài 2: Tối ưu Prompt – Debug NullPointerException (Java)

## 1. Prompt đã tối ưu (5 thành phần)

### Prompt:

Bạn hãy đóng vai trò là một **Java Debugging Expert (chuyên gia gỡ lỗi Java)** có kinh nghiệm phân tích lỗi runtime trong hệ thống production.

Tôi đang gặp lỗi khi chạy chương trình Java dưới đây. Hãy giúp tôi phân tích và sửa lỗi.

---

## Mã nguồn gây lỗi:
```java
import java.util.List;

public class UserManager {

    private List<String> users; // chưa được khởi tạo nên bị null

    public void addUser(String user) {
        users.add(user); // dòng gây lỗi NullPointerException
    }
}
```

---

## Stack Trace:
```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.util.List.add(Object)" because "this.users" is null
    at UserManager.addUser(UserManager.java:7)
    at Main.main(Main.java:6)
```

---

## Yêu cầu xử lý:

1. Phân tích **nguyên nhân gốc rễ (Root Cause)** của lỗi NullPointerException.
2. Giải thích vì sao lỗi xảy ra dựa trên Stack Trace.
3. Đề xuất cách sửa **an toàn nhất theo chuẩn OOP (Encapsulation)**.
4. Không sửa theo hướng “tùy tiện public field” hoặc phá vỡ thiết kế lớp.
5. Cách sửa đúng phải đảm bảo:
    - users luôn được khởi tạo hợp lệ
    - tránh NullPointerException trong mọi trường hợp
    - giữ nguyên thiết kế hướng đối tượng

---

## Yêu cầu đầu ra:

- Giải thích lỗi rõ ràng, có phân tích
- Đưa ra code Java đã sửa hoàn chỉnh
- Code phải an toàn, đúng OOP

---

## 2. Code Java sau khi sửa (kết quả mong muốn)

```java
import java.util.ArrayList;
import java.util.List;

public class UserManager {

    private List<String> users;

    public UserManager() {
        this.users = new ArrayList<>();
    }

    public void addUser(String user) {
        if (user == null || user.isEmpty()) {
            throw new IllegalArgumentException("User không hợp lệ");
        }
        users.add(user);
    }

    public List<String> getUsers() {
        return new ArrayList<>(users);
    }
}
```