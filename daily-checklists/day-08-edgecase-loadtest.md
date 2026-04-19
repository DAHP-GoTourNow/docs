# Day 08 - Edge-case + Concurrent Test Checklist

## Muc tieu ngay
- Danh vao edge-case va test tai cao cho luong booking-payment.
- Khoa cac loi nguy hiem truoc feature freeze.

## Checklist theo nguoi

### The Anh
- [ ] To chuc E2E test session va triage blocker.
- [ ] Kiem tra log correlationId xuyen chuoi request/event.
- [ ] Chot danh sach bug P1/P2 can fix ngay.

### Tuan Anh
- [ ] Ho tro endpoint promotion/review can ban (neu con thieu).
- [ ] Verify search behavior khi data update nhanh.
- [ ] Toi uu query va field projection de giam latency.

### Viet Cuong
- [ ] Test concurrent dat tour (nhieu request cung tour).
- [ ] Xac nhan khong overbooking.
- [ ] Verify compensation flow khi payment timeout/fail.

### Duc Hau
- [ ] Test callback duplicate nhieu lan.
- [ ] Kiem tra reconciliation log du thong tin.
- [ ] Validate refund flow khong pha trang thai booking.

## Deliverables bat buoc cuoi ngay
- [ ] Bao cao test concurrent + ket qua overbooking = 0.
- [ ] Danh sach edge-case da pass/fail ro rang.
- [ ] Bug list P1/P2 co owner va ETA fix.

## Gate check
- [ ] Neu overbooking > 0 thi khong duoc sang Day 9.
- [ ] Neu callback duplicate tao giao dich moi thi rollback fix ngay.
