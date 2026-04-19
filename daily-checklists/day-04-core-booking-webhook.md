# Day 04 - Core CRUD Full + Booking Logic + Webhook Verify

## Muc tieu ngay
- Core CRUD day du cho tour/departure/price.
- Booking status machine ban dau.
- Payment webhook verify + idempotency hoat dong.

## Checklist theo nguoi

### The Anh
- [ ] Chot route wiring identity/core/booking/payment qua gateway.
- [ ] Review merge middleware auth va error format.
- [ ] Kiem tra response schema khop OpenAPI.

### Tuan Anh
- [ ] Core CRUD Tour.
- [ ] Core CRUD Departure.
- [ ] Core CRUD PriceConfig.
- [ ] Constraint: price > 0, quantity >= 0.

### Viet Cuong
- [ ] Booking status machine: pending -> confirmed/cancelled.
- [ ] Validate booking payload.
- [ ] Prevent orphan records trong transaction ban dau.

### Duc Hau
- [ ] Webhook endpoint verify signature.
- [ ] Idempotency key check cho callback duplicate.
- [ ] Mapping payment status pending/success/failed.

## Deliverables bat buoc cuoi ngay
- [ ] Core CRUD tour/departure/price hoat dong.
- [ ] Booking create tra status pending.
- [ ] Callback duplicate khong tao giao dich moi.

## Gate check
- [ ] Unit test webhook idempotency pass.
- [ ] Booking va payment status enum dong bo.
