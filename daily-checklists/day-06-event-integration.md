# Day 06 - Event Integration Checklist

## Muc tieu ngay
- Tich hop event lien service som truoc khi rap Saga.
- Smoke test event bus Booking->Payment va outbox-worker index trong Core.

## Checklist theo nguoi

### The Anh
- [ ] Kiem tra broker topic/queue setup dung naming convention.
- [ ] Tao script smoke test pub/sub cho team.
- [ ] Kiem tra retry + DLQ config can ban.

### Tuan Anh
- [ ] Core publish TourUpdated event.
- [ ] Core worker consume outbox TourUpdated va cap nhat index.
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
- [ ] Outbox->Index trong Core chay 1 vong thanh cong.
- [ ] Event Booking->Payment->Booking chay mock thanh cong.
- [ ] Co dashboard/log chung minh event da di qua broker.

## Gate check
- [ ] Event payload docs cap nhat dung version.
- [ ] Khong co event critical chua co retry strategy.
