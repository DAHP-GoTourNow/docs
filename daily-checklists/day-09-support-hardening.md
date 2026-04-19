# Day 09 - Support Service + Hardening Checklist

## Muc tieu ngay
- Hoan tat Support Service ban co ban.
- Freeze feature, tap trung hardening va regression.

## Checklist theo nguoi

### The Anh
- [ ] RC checklist va security review toan he thong.
- [ ] Kiem tra CORS, rate limit, auth middleware route quan trong.
- [ ] Freeze feature policy (chi bugfix).

### Tuan Anh
- [ ] Bugfix P1/P2 Core + Search.
- [ ] Verify constraints schema va migration final.
- [ ] Kiem tra lai docs API neu co thay doi payload.

### Viet Cuong
- [ ] Bugfix P1 Booking + lock/saga logs.
- [ ] Kiem tra lai cancellation va compensation flow.
- [ ] Chuan hoa test cases booking regression.

### Duc Hau
- [ ] Implement Support Service: ticket API co ban.
- [ ] Implement chat API + pagination.
- [ ] Kiem tra Payment + Support khong xung dot route.

## Deliverables bat buoc cuoi ngay
- [ ] Support API chay duoc end-to-end co ban.
- [ ] Regression test pass cho auth/core/search/booking/payment.
- [ ] Feature freeze duoc thong bao ro trong team.

## Gate check
- [ ] Khong merge feature moi sau 17h Day 9.
- [ ] Tat ca bug P1 phai co owner + ETA fix Day 10.
