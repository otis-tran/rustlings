# 🦀 Rust

## 🚀 Giới thiệu
---

## 📝 Các cách sử dụng `println!`

### 1️⃣ Chèn giá trị vào chuỗi bằng `{}`
```rust
println!("Hello {}!", "Rust");
```

### 2️⃣ Truyền tham số theo thứ tự
```rust
println!("Hello {}, welcome to {}!", "Alice", "Rust");
```

### 3️⃣ Sử dụng positional arguments
```rust
println!("{1} is learning {0}", "Rust", "Bob");
```

### 4️⃣ Sử dụng named arguments
```rust
println!("Hello {name}, you are learning {language}", name="Bob", language="Rust");
```

# 🦀 Rust - Variables

Trong Rust, biến có thể là **immutable** hoặc **mutable** 

---

## 🔹 Biến Immutable vs Mutable
- **Immutable (mặc định):** Không thể thay đổi giá trị sau khi gán.
- **Mutable:** Dùng `let mut` để có thể gán giá trị mới.

---

## ⚠️ Lưu ý
- Không thể thay đổi kiểu dữ liệu của biến đã khai báo.
---

# 🦀 [Stack & Heap](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)

> Ownership có liên quan đến Stack và Heap

Stack và Heap đều là các phần của bộ nhớ (được sử dụng khi chạy chương trình)

## 🛢️ Stack
Stack hoạt động theo nguyên tắc LIFO (last in, first out)

> Hãy tưởng tượng một chồng tô: khi bạn thêm nhiều tô hơn, bạn đặt chúng lên trên cùng của chồng, và khi bạn cần một cái tô, bạn lấy cái trên cùng. 
> 
>Việc thêm hoặc lấy tô ở giữa hoặc dưới cùng sẽ không hiệu quả!


- Push: Thêm dữ liệu vào stack
- Pop: Loại bỏ dữ liệu khỏi stack

📌 Tất cả dữ liệu được lưu trữ trên stack phải có kích thước cố định và đã biết trước.

> Dữ liệu có kích thước không xác định khi biên dịch hoặc có thể thay đổi kích thước phải được lưu trữ trên Heap

## 🏗️ Heap
Heap thì kém tổ chức hơn Stack: khi đặt dữ liệu lên heap, cần cấp phát một lượng bộ nhớ nhất định.

📌 **Quá trình Memory Allocation** (Cấp phát bộ nhớ)
1. Bộ cấp phát bộ nhớ (memory allocator) sẽ tìm một vị trí trống, đủ lớn trong heap
2. Đánh dấu vị trí đó là đang được sử dụng
3. Trả về một con trỏ (pointer) – địa chỉ của vùng nhớ vừa cấp phát

> Việc push dữ liệu lên stack không được coi là cấp phát bộ nhớ (push con trỏ vào stack). 
> Vì con trỏ trỏ đến heap có kích thước cố định và đã biết, bạn có thể lưu con trỏ này trên stack, nhưng khi muốn truy cập dữ liệu thực tế, bạn phải theo con trỏ đó.

📖 Hãy tưởng tượng mình đang vào một nhà hàng. 
1. Khi đến nơi, mình nói với nhân viên số lượng người trong nhóm
2. Nhân viên sẽ tìm một bàn trống đủ chỗ rồi dẫn mình đến đó. 
3. Nếu có người đến muộn, họ có thể hỏi nhân viên vị trí bàn của bạn để tìm đến.

> Nhân viên phục vụ chính là memory allocator

## ⚡ So sánh hiệu suất

- ✅ **Push vào stack nhanh hơn** cấp phát trên heap, vì memory allocator không cần tìm vị trí trống – vị trí tiếp theo luôn ở trên cùng của stack.
- 🚀 **Cấp phát trên heap chậm hơn** vì memory allocator phải tìm không gian đủ lớn để lưu dữ liệu và sau đó thực hiện quản lý để chuẩn bị cho lần cấp phát tiếp theo.
- 🔍 **Truy cập dữ liệu trong heap chậm hơn** so với stack vì phải theo một con trỏ để đến dữ liệu thực tế.
- 🏎 Bộ xử lý hiện đại sẽ hoạt động nhanh hơn nếu nó truy cập dữ liệu gần nhau trong bộ nhớ.

> 📌 **Tưởng tượng một người phục vụ nhà hàng nhận order từ nhiều bàn khác nhau:**
>
> - Cách nhanh nhất là lấy tất cả order từ **một bàn** trước khi chuyển sang bàn tiếp theo.
> - Nếu người phục vụ lấy order từ bàn A, rồi bàn B, rồi quay lại bàn A, quá trình này sẽ mất nhiều thời gian hơn.
> - Tương tự, bộ xử lý sẽ **hiệu quả hơn** khi làm việc với dữ liệu **gần nhau** trong bộ nhớ (**stack**) thay vì theo con trỏ đến dữ liệu ở vị trí xa hơn (**heap**).

## 🔗 Liên quan đến Ownership

- Khi một **hàm được gọi**, các **biến cục bộ** và **tham số truyền vào** sẽ được **push lên stack**.
- Khi hàm kết thúc, chúng **bị pop khỏi stack** một cách tự động.
- 🔥 Việc theo dõi xem phần nào của code đang sử dụng dữ liệu nào trên heap, giảm thiểu dữ liệu trùng lặp trên heap và dọn dẹp dữ liệu không còn sử dụng để tránh tràn bộ nhớ là những vấn đề mà quyền sở hữu (ownership) giải quyết.

> **Ownership giúp:**  
> ✅ Theo dõi dữ liệu nào đang được sử dụng.     
> ✅ Giảm thiểu dữ liệu trùng lặp.       
> ✅ Dọn dẹp dữ liệu không cần thiết để tránh **memory leak**.

> **🎯 Kết luận:**
> - Sau khi hiểu Ownership, bạn **không cần phải lo lắng quá nhiều về stack và heap**.
> - Nhưng biết rằng **mục tiêu chính của Ownership là quản lý dữ liệu trên heap** sẽ giúp bạn hiểu rõ hơn về cách Rust hoạt động. 🚀

---
