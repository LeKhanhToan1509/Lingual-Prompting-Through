
## Cách đánh giá

### ✅ 1. So sánh đúng/sai câu hỏi MMLU
**Chỉ số dùng:** Accuracy
- **Dạng đề:** Trắc nghiệm chọn A/B/C/D
- **Ví dụ:**

| Câu hỏi | Đáp án đúng | Mô hình chọn | Đúng/Sai |
|---------|-------------|--------------|----------|
| What is 2 + 2? | A (4) | A (4) | ✅ |
| What is the capital of France? | C (Paris) | B (London) | ❌ |

**Tính accuracy:**
$Accuracy = \frac{1 \text{ (câu đúng)}}{2 \text{ (tổng số câu)}} = 50\%$

### ✍️ 2. Nếu sinh câu trả lời tự do
**Chỉ số dùng:** Exact Match (EM) và F1 Score
- **Dạng đề:** Mô hình tự sinh câu trả lời, ví dụ QA hoặc ngắn gọn.

➤ **Exact Match (EM)**

| Câu hỏi | Đáp án mẫu | Mô hình trả lời | EM |
|---------|------------|----------------|-----|
| Ai là tác giả của Truyện Kiều? | Nguyễn Du | Nguyễn Du | ✅ 1 |
| Ai viết "Lão Hạc"? | Nam Cao | Nhà văn Nam Cao | ❌ 0 |

→ Chỉ khi nào trùng 100% từ thì mới tính là đúng

➤ **F1 Score**

| Đáp án mẫu | Mô hình trả lời | F1 |
|------------|----------------|-----|
| Nguyễn Du | Nhà thơ Nguyễn Du | ~0.8 |
| Nam Cao | Nhà văn Nam Cao | ~0.8 |
| Hồ Chí Minh | Bác Hồ | thấp (~0.3) |

→ F1 linh hoạt hơn, miễn có chứa từ đúng là tính điểm.

### 🌐 3. Dịch đa ngôn ngữ, đánh giá chất lượng dịch
**Chỉ số dùng:** BLEU hoặc BERTScore
- **Dạng đề:** Câu hỏi đã dịch ra ngôn ngữ khác, cần so sánh với bản chuẩn

➤ **BLEU**
Đánh giá độ giống n-gram giữa 2 câu

| Ground truth | Translation | BLEU |
|--------------|-------------|------|
| Tôi đang ăn cơm | Tôi đang dùng cơm | ~0.7 |
| Tôi đang học bài | Tôi học | ~0.3 |
| Anh ấy là bác sĩ | Anh ta là thầy thuốc | ~0.2 |

BLEU thấp nếu cấu trúc khác hẳn nhau dù ý tương tự

➤ **BERTScore**
So sánh embedding câu, hiểu ngữ nghĩa

| Ground truth | Translation | BERTScore |
|--------------|-------------|-----------|
| Tôi đang ăn cơm | Tôi đang dùng cơm | ✅ 0.92 |
| Anh ấy là bác sĩ | Anh ta là thầy thuốc | ✅ 0.88 |

→ BERTScore cao hơn BLEU trong ngữ cảnh nghĩa tương tự

### 🧠 4. So sánh đầu ra mang tính ngữ nghĩa
**Chỉ số dùng:** BERTScore
- **Ví dụ bài toán:** Mô hình giải thích/biện luận về một khái niệm

| Ground truth (mẫu) | Output mô hình | BERTScore |
|--------------------|----------------|-----------|
| "Nguyên nhân chính là do thời tiết khắc nghiệt gây hạn hán." | "Hạn hán xảy ra vì thời tiết quá khô và nắng nóng kéo dài." | ✅ ~0.89 |
| "Bệnh nhân bị sốt xuất huyết cần truyền dịch." | "Người bệnh cần được truyền nước khi bị sốt xuất huyết." | ✅ ~0.91 |

→ Những câu này không giống từ ngữ nhưng cùng nghĩa, chỉ BERTScore mới đánh giá tốt.

## ✅ Tổng hợp gọn

| Mục tiêu | Chỉ số | Ví dụ đánh giá |
|----------|--------|----------------|
| MMLU / trắc nghiệm chọn đáp án | Accuracy | Trả lời đúng A/B/C/D => tính tỉ lệ đúng |
| Trả lời tự do (short QA) | Exact Match / F1 | Câu trả lời giống hoàn toàn hoặc chứa từ đúng |
| Kiểm tra chất lượng dịch sang ngôn ngữ | BLEU / BERTScore | So sánh bản dịch với bản chuẩn |
| So sánh kết quả có cùng ý nhưng khác từ | BERTScore | Đo mức độ đồng nghĩa giữa 2 câu (embedding) |
