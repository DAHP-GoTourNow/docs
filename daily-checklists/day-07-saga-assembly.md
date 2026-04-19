# Day 07 - Saga Assembly Checklist

## Muc tieu ngay
- Rap luong Saga booking-payment tren du lieu that.
- Co flow compensation can ban khi payment fail.

## Checklist theo nguoi

### The Anh
- [ ] Review architecture flow Saga va approve event contracts cuoi.
- [ ] Hardening CORS, rate limit, security headers o gateway.
- [ ] Chot smoke test checklist cho Saga.

### Tuan Anh
- [ ] Tuning search cache Redis cho query hot.
- [ ] Ho tro data setup de test Saga edge cases.
- [ ] Kiem tra Core data consistency khi booking/payment update.

### Viet Cuong
- [ ] Booking consume PaymentSucceeded -> set confirmed.
- [ ] Booking consume PaymentFailed -> set cancelled.
- [ ] Compensation flow: release reservation lock khi fail.

### Duc Hau
- [ ] Payment publish success/fail dung contract.
- [ ] Refund API co ban.
- [ ] Ensure callback duplicate khong trigger Saga 2 lan.

## Deliverables bat buoc cuoi ngay
- [ ] Saga happy path pass: booking -> payment success -> confirmed.
- [ ] Saga fail path pass: booking -> payment fail -> cancelled + unlock.
- [ ] Security gate can ban cua gateway pass.

## Gate check
- [ ] Khong con trang thai booking "treo" khong xu ly.
- [ ] Co log trace full chain theo correlationId.
