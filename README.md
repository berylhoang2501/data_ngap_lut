# data_ngap_lut

[1] DỮ LIỆU ĐẦU VÀO
    ├─ Chuỗi thời gian mực nước:
    │   ├─ H Phú An Max (m)
    │   └─ H Nhà Bè Max (m)
    │
    ├─ Lớp điểm độ cao:
    │   └─ DOCAO + Spot + geometry
    │
    ├─ Lớp ranh giới hành chính:
    │   └─ quận/huyện + geometry
    │
    ├─ Lớp sử dụng đất:
    │   └─ Loai_SDD + geometry
    │
    └─ Lớp thổ nhưỡng:
        └─ LoaiThoNhuong + geometry


[2] TIỀN XỬ LÝ & CHUẨN HÓA
    ├─ Chuẩn hóa CRS cho tất cả lớp không gian
    ├─ Tách geometry → tọa độ X, Y
    ├─ Làm sạch tên cột, kiểu dữ liệu
    ├─ Đồng bộ thời gian chuỗi mực nước
    └─ Spatial join:
        ├─ điểm độ cao ↔ quận/huyện
        ├─ điểm độ cao ↔ land use
        └─ điểm độ cao ↔ soil


[3] XÂY DỰNG Hmax ƯỚC TÍNH TẠI MỖI ĐIỂM
    ├─ Đầu vào lõi:
    │   ├─ H Phú An Max
    │   ├─ H Nhà Bè Max
    │   └─ vị trí điểm (X, Y)
    │
    ├─ Hiệu chỉnh không gian:
    │   ├─ theo quận/huyện
    │   ├─ theo land use (nếu cần)
    │   └─ theo soil (nếu cần, mức phụ)
    │
    └─ Kết quả:
        └─ Hmax_est(point, date)


[4] TÍNH ĐỘ SÂU NGẬP
    └─ FloodDepth = max(0, Hmax_est - DOCAO)


[5] PHÂN LOẠI NGUY CƠ NGẬP
    ├─ 0 m                → Không ngập
    ├─ 0 - 0.2 m          → Nguy cơ thấp
    ├─ 0.2 - 0.5 m        → Nguy cơ trung bình
    └─ > 0.5 m            → Nguy cơ cao


[6] TỔNG HỢP KẾT QUẢ
    ├─ Theo điểm
    ├─ Theo quận/huyện
    ├─ Theo loại sử dụng đất
    └─ Theo loại thổ nhưỡng


[7] ĐẦU RA CUỐI
    ├─ Bảng Hmax_est tại từng điểm
    ├─ Bảng FloodDepth tại từng điểm
    ├─ Bản đồ nguy cơ ngập theo quận/huyện
    ├─ Bản đồ nguy cơ ngập theo loại sử dụng đất
    └─ Bảng thống kê vùng rủi ro cao


