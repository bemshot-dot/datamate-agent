# SổSách AI — DataMate Agent

> *Hỏi là có số, sai thì không nói.*

Giải pháp cho thử thách **DataMate – Talking To Your Data Through Agentic AI** tại **Zalo AI Challenge 2026**.

SổSách AI là một AI agent trả lời câu hỏi tiếng Việt đời thường trên dữ liệu có cấu trúc (CSV, Excel, SQLite) của các doanh nghiệp nhỏ Việt Nam — tạp hóa, quán cà phê, nhà thuốc, cửa hàng vật liệu xây dựng... Agent trả về đáp án chính xác, hoặc từ chối trả lời khi dữ liệu không đủ để trả lời.

## Ví dụ

**Input** (`questions.jsonl`):

```json
{"id": "q_06de33fa21cc", "business_id": "biz_118", "question": "sp bán dc nhiều nhất tuần rồi là gì", "as_of_date": "2026-03-04"}
```

**Output** (`submission.jsonl`):

```json
{"id": "q_06de33fa21cc", "type": "string", "answer": "Xi măng Hà Tiên PCB40 bao 50kg"}
```

## Ràng buộc chính

| Hạng mục | Yêu cầu |
|---|---|
| Mô hình | Tổng ≤ 15B tham số, công bố trước 01/10/2026 |
| Chạy | Hoàn toàn offline trong Docker, không mạng |
| Phần cứng | 2 × RTX 5090 (64 GB VRAM), 512 GB RAM |
| Thời gian | Toàn bộ private test ≤ 6 giờ |
| Chấm điểm | Penalized Accuracy — sai bị phạt, `abstain` không bị phạt |

## Hướng tiếp cận

1. **Tiền xử lý** — nạp dữ liệu mỗi doanh nghiệp vào DuckDB, tự lập hồ sơ schema.
2. **Hàm nghiệp vụ** — đơn hợp lệ, doanh thu, khoảng thời gian, khoảng Tết... tham số hóa theo `rulebook.md`.
3. **Agent** — LLM sinh code SQL/Python → thực thi → tự sửa lỗi → định dạng đáp án.
4. **Kiểm soát rủi ro** — kiểm tra chéo nhiều lời giải; không chắc chắn thì `abstain`.

## Cách chạy

```bash
bash predict.sh   # đọc /data, ghi /result/submission.jsonl và /result/logs/
```

## Trạng thái

🚧 Đang phát triển.

## Mốc thời gian

- **16/11/2026** — Nộp Docker image
- **20–23/11/2026** — Private test
