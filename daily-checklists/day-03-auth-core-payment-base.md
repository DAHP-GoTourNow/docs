# Day 03 - Identity + Core + Payment Base Checklist

## Muc tieu ngay
- Identity flow co ban chay.
- Core CRUD can ban bat dau chay.
- Payment intent API co ban chay.

## Checklist theo nguoi

### The Anh
- [ ] Hoan thien Identity API: register/login/refresh/logout.
- [ ] Auth middleware validate JWT cho route can bao ve.
- [ ] Review va merge PR Core/Booking/Payment phien ban dau.

### Tuan Anh
- [ ] Core CRUD Category.
- [ ] Core CRUD Destination.
- [ ] Validation request body theo schema.

### Viet Cuong
- [ ] Booking create/get API ban dau (dung mock Core data neu can).
- [ ] Luu status pending mac dinh.
- [ ] Log theo correlationId.

### Duc Hau
- [ ] Payment intent create API.
- [ ] Luu transaction ban dau.
- [ ] Mapping field bookingId, amount, status.

## Deliverables bat buoc cuoi ngay
- [ ] Dang nhap lay token va goi duoc 1 protected API.
- [ ] Core CRUD category/destination test pass.
- [ ] Payment intent co response hop le va luu DB.

## Gate check
- [ ] Khong co endpoint critical tra 500 khong debug duoc.
- [ ] CorrelationId co trong log 3 service: gateway, core, payment.
