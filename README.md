# AI-Enabled Threat Detection — Review & Demo (Network Intrusion Detection)

> Đồ án môn **Bảo mật Hệ thống Thông tin Hiện đại** — Chương trình Thạc sĩ Công nghệ
> Thông tin, Trường Đại học Công nghệ TP.HCM (HUTECH), 04/2025.

Khảo sát và đánh giá vai trò của **AI/ML trong an ninh mạng** (dựa trên paper *AI Enabled
Threat Detection*, Dhanushkodi & Thejas, 2024), kèm một **demo phát hiện xâm nhập mạng
(Network Intrusion Detection)** trên bộ dữ liệu **NSL-KDD**, và một khung mô phỏng tấn
công để sinh dữ liệu lưu lượng huấn luyện.

> ⚠️ **Mục đích phòng thủ & học thuật.** Phần mô phỏng tấn công chỉ chạy trong môi trường
> lab cô lập để sinh dữ liệu cho mô hình phát hiện (defensive IDS) — không nhằm tấn công
> hệ thống thực.

## Nội dung

1. **Tổng quan** — bối cảnh mối đe dọa (Phishing, Ransomware, DDoS, APT, Zero-day) và giới
   hạn của phương pháp dựa-luật tĩnh; vì sao AI là giải pháp chủ động, thích ứng.
2. **Mục tiêu & phạm vi** — khảo sát các mô hình AI (SVM, Random Forest, CNN, RNN, GANs…),
   đánh giá thực nghiệm, đề xuất hướng Explainable AI.
3. **Nền tảng kiến thức** — tổng hợp các nghiên cứu: deep learning, GAN cho IDS, XAI cho
   Industry 5.0, AI Shield Framework…
4. **Demo** — phân loại lưu lượng *bình thường / tấn công* trên NSL-KDD.
5. **Thảo luận & Paper review** — điểm mạnh/hạn chế của paper gốc.

## Pipeline tiền xử lý dữ liệu

```
Làm sạch → Trích xuất đặc trưng → Chuẩn hóa (Min-Max / Standardization)
   → Tăng cường & giảm chiều (PCA, data augmentation) → Chuyển đổi (log transform, encoding)
```

## Các nhóm mô hình AI được khảo sát

| Nhóm | Mô hình | Vai trò trong an ninh mạng |
|------|---------|----------------------------|
| **Machine Learning** | SVM, Random Forest | Phân loại với ranh giới rõ ràng; ổn định trên dữ liệu phức tạp |
| **Deep Learning** | CNN, RNN, GAN | Nhận dạng mẫu không gian/thời gian; sinh dữ liệu tấn công mô phỏng |
| **Hybrid / Explainable** | Ensemble, Transformer, **XAI (SHAP)** | Tăng độ chính xác + minh bạch quyết định (Industry 5.0) |

**Ví dụ XAI (SHAP)** cho một cảnh báo tấn công:
`Protocol=FTP (+0.25)`, `Packet size>1000B (+0.40)`, `Destination IP=suspicious (+0.35)`,
`Time of day=unusual (+0.15)` → tổng điểm đủ cao để gắn nhãn *"attack"*.

## Demo: AI-Powered Network Intrusion Detection (NSL-KDD)

- **Dataset:** NSL-KDD — chuẩn đánh giá hệ thống phát hiện xâm nhập (IDS).
- **Đặc trưng:** 41 thuộc tính (`duration`, `protocol_type`, `service`, `flag`, `src_bytes`,
  `dst_bytes`, `land`, …) + nhãn lớp.
- **4 loại tấn công chính:** DoS, Probe, R2L, U2R.
- **Quy trình:** tiền xử lý → train/test split → tuning siêu tham số → cross-validation →
  đánh giá đa chỉ số (accuracy, precision/recall, …).

## Khung mô phỏng tấn công (sinh dữ liệu)

```
Metasploit (tấn công máy mục tiêu có lỗ hổng, vd SMB)
   → Wireshark (bắt lưu lượng)
   → CICFlowMeter (trích đặc trưng luồng)
   → Huấn luyện mô hình AI phát hiện tấn công
```

## Cài đặt & chạy demo

```bash
pip install scikit-learn pandas numpy matplotlib seaborn shap
# Tải NSL-KDD, chạy notebook/script huấn luyện IDS
```

> Cập nhật đường dẫn dataset và tên file notebook cho khớp repo.

## Kết luận

- AI giữ vai trò trung tâm trong an ninh mạng hiện đại; **Explainability** và **Resilience**
  là hai trọng tâm.
- GANs, Transformers, Explainable AI cho hiệu quả cao; AI vượt trội so với giải pháp
  dựa-luật truyền thống.
- Thách thức: mất cân bằng dữ liệu, chi phí tính toán, tích hợp XAI.

### Hướng phát triển
Mô hình AI minh bạch + học liên tục; mở rộng sang edge computing, quantum, blockchain và
hệ thống phân tán.

## Tài liệu tham khảo

- Kavitha Dhanushkodi, S. Thejas (2024). *AI Enabled Threat Detection: Leveraging Artificial
  Intelligence for Advanced Security and Cyber Threat Mitigation.*

## Nhóm thực hiện

Nguyễn Ngọc Đỉnh · Kiều Văn Đoàn — GVHD: TS. Huỳnh Quốc Bảo
