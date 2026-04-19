# Day 01 - Design Freeze Checklist

## Muc tieu ngay
- Freeze architecture, schema, API contracts, event contracts.
- Khoi tao Postman Mock Server co URL that.

## Checklist theo nguoi

### The Anh
- [ ] Chot boundary service v1: gateway, identity, core, search, booking, payment, support.
- [ ] Chot convention API: status code, error format, pagination, versioning.
- [ ] Import OpenAPI vao Postman va tao Mock Server URL.
- [ ] Chot naming convention: camelCase, enum, date object.

### Tuan Anh
- [ ] Chot entities Core: category, tour, destination, departure, priceConfig.
- [ ] Chot constraint: price > 0, quantity >= 0, required fields.
- [ ] Tao mock response Core CRUD tren Postman collection.

### Viet Cuong
- [ ] Chot entities Booking: booking, passenger, cancellation, reservationLock.
- [ ] Chot status machine booking: pending, confirmed, cancelled.
- [ ] Tao mock response booking create/get/cancel.

### Duc Hau
- [ ] Chot entities Payment: intent, transaction, webhook log, refund.
- [ ] Chot callback payload va idempotency key strategy.
- [ ] Tao mock response payment intent/webhook/refund.

## Deliverables bat buoc cuoi ngay
- [ ] File OpenAPI draft v1 cho cac service.
- [ ] Link Postman Mock Server URL cho ca team.
- [ ] Event contract draft: BookingCreated, PaymentSucceeded, PaymentFailed.
- [ ] Minutes architecture sign-off.

## Gate check
- [ ] Team dong y khong doi schema lon sau Day 1.
- [ ] Tat ca dependency lien service da co mock endpoint.
