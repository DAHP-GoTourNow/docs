# Day 06 - Event Integration Checklist

## Muc tieu ngay
- Tich hop event lien service som truoc khi rap Saga.
- Smoke test event bus Core->Search va Booking->Payment.

## Checklist theo nguoi

### The Anh
- [ ] Kiem tra broker topic/queue setup dung naming convention.
- [ ] Tao script smoke test pub/sub cho team.
- [ ] Kiem tra retry + DLQ config can ban.

### Tuan Anh
- [ ] Core publish TourUpdated event.
- [ ] Search consume TourUpdated va cap nhat index.
- [ ] Ghi log event co correlationId.

### Viet Cuong
- [ ] Booking publish BookingCreated event.
- [ ] Booking listen PaymentSucceeded/Failed placeholder handler.
- [ ] Snapshot gia/promo luu vao booking khi create.

### Duc Hau
- [ ] Payment consume BookingCreated event.
- [ ] Payment publish PaymentSucceeded/Failed event.
- [ ] Kiem tra idempotency event consumer.

## Deliverables bat buoc cuoi ngay
- [ ] Event Core->Search chay 1 vong thanh cong.
- [ ] Event Booking->Payment->Booking chay mock thanh cong.
- [ ] Co dashboard/log chung minh event da di qua broker.

## Gate check
- [ ] Event payload docs cap nhat dung version.
- [ ] Khong co event critical chua co retry strategy.
