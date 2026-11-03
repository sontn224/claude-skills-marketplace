# Thang chấm rủi ro mẫu (5 x 5)

Đây là thang mẫu. Tổ chức có thang riêng thì dùng thang đó và ghi rõ trong register. Mọi điểm do AI chấm vẫn là đề xuất `[GIẢ ĐỊNH]` đến khi BA/PM xác nhận.

## Khả năng xảy ra (P)
| Điểm | Mức | Mô tả |
|---|---|---|
| 1 | Rất khó | Cần nhiều điều kiện cùng xảy ra; chưa có dấu hiệu nào trong nguồn |
| 2 | Khó | Có thể xảy ra nhưng nguồn chưa có dấu hiệu |
| 3 | Có thể | Nguồn có dấu hiệu gián tiếp hoặc điều kiện kích hoạt còn mở |
| 4 | Dễ xảy ra | Nguồn nêu điều kiện kích hoạt đã tồn tại và chưa có biện pháp |
| 5 | Gần như chắc chắn | Điều kiện đã xảy ra một phần hoặc là hệ quả trực tiếp của ràng buộc đã biết |

## Tác động (I)
Chấm theo hậu quả nặng nhất lên mục tiêu của kế hoạch (tiến độ, phạm vi, chi phí, chất lượng, mục tiêu kinh doanh). Neo theo tiến độ khi nguồn không nói gì khác.

| Điểm | Mức | Neo theo tiến độ | Neo theo phạm vi / mục tiêu |
|---|---|---|---|
| 1 | Không đáng kể | Trễ không quá vài ngày, tự hấp thụ được | Không đổi phạm vi |
| 2 | Nhỏ | Trễ khoảng một tuần | Thay đổi nhỏ ở một tính năng phụ |
| 3 | Vừa | Trễ vài tuần, phải điều chỉnh kế hoạch sprint | Cắt hoặc hoãn một tính năng phụ |
| 4 | Lớn | Trễ làm lệch một mốc quan trọng | Cắt hoặc hoãn tính năng chính; mục tiêu kinh doanh giảm rõ |
| 5 | Nghiêm trọng | Lỡ mốc cố định hoặc không thể hoàn thành phase | Mất mục tiêu chính của phase; phải làm lại phần lớn |

Các neo thời gian ở trên là thang mẫu, thay bằng số ngày thật của kế hoạch khi có.

## Điểm và mức
Điểm = P x I.

| Điểm | Mức | Yêu cầu xử lý |
|---|---|---|
| 1-4 | Thấp | Ghi nhận, review định kỳ |
| 5-9 | Trung bình | Có hành động ứng phó và người phụ trách |
| 10-14 | Cao | Có hành động, kế hoạch dự phòng và trigger theo dõi mỗi sprint |
| 15-25 | Rất cao | Báo sponsor; xử lý trước; review từng tuần |

## Chiến lược ứng phó
| Chiến lược | Ý nghĩa | Dùng khi |
|---|---|---|
| Avoid | Loại bỏ nguyên nhân (đổi phạm vi, đổi cách làm) | Có thể bỏ được nguồn rủi ro |
| Mitigate | Giảm khả năng hoặc tác động | Không bỏ được nhưng giảm được |
| Transfer | Chuyển sang bên khác (nhà cung cấp, hợp đồng) | Bên khác kiểm soát tốt hơn |
| Accept | Chấp nhận, có hoặc không có dự phòng | Điểm thấp hoặc chi phí xử lý cao hơn thiệt hại |
| Exploit / Enhance | Dành cho cơ hội: bảo đảm xảy ra / tăng khả năng, tăng lợi ích | Loại Opportunity |

## Quy tắc viết trigger
- Là dấu hiệu quan sát được và có thời điểm (ví dụ "cuối sprint hiện tại chưa nhận được tài liệu X").
- Nêu ai theo dõi và đo ở đâu. Không có số liệu trong nguồn thì dùng điều kiện có/không, không tự đặt ngưỡng số.
- Không dùng "khi có vấn đề", "khi cần".

## Quy tắc chọn người phụ trách
- Một vai duy nhất, có quyền hoặc ảnh hưởng đủ để thực hiện hành động ứng phó.
- Vai từ nguồn dùng nguyên văn; vai dự án chưa có trong nguồn (PM, BA, Tech lead) gắn `[GIẢ ĐỊNH]`.
- Người phụ trách theo dõi và điều phối, không nhất thiết là người làm toàn bộ hành động.
