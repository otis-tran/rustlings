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

