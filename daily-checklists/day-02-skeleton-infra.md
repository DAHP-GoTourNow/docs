# Day 02 - Skeleton + Infra Checklist

## Muc tieu ngay
- Dung duoc skeleton tat ca service.
- Setup Docker Compose hybrid local cho backing services.
- Bat buoc co Correlation ID middleware o gateway.

## Checklist theo nguoi

### The Anh
- [ ] Tao docker-compose chi chua: postgres, mongo, redis, broker, elasticsearch.
- [ ] Xac nhan service code chay host localhost (khong dockerize app code).
- [ ] Dung gateway skeleton route /auth /core /search /booking /payment /support.
- [ ] Tao middleware sinh X-Correlation-ID (UUID) neu chua co header.
- [ ] Gateway pass X-Correlation-ID xuong downstream.

### Tuan Anh
- [ ] Khoi tao Core service project structure.
- [ ] Tao migration/schema ban dau cho Core entities.
- [ ] Tao endpoint health + base CRUD placeholder.

### Viet Cuong
- [ ] Khoi tao Booking service project structure.
- [ ] Tao schema bookings/passengers/cancellations/reservation_locks.
- [ ] Tao endpoint health + create/get placeholder.

### Duc Hau
- [ ] Khoi tao Payment service project structure.
- [ ] Tao schema payment intents/transactions/webhook logs.
- [ ] Tao endpoint health + create intent placeholder.

## Deliverables bat buoc cuoi ngay
- [ ] Compose up thanh cong tren may cua it nhat 2 thanh vien.
- [ ] Gateway route duoc den tat ca service health endpoint.
- [ ] Correlation ID hien trong log gateway va 1 service bat ky.

## Gate check
- [ ] Moi thanh vien co script run local 1 lenh.
- [ ] Khong co blocker ha tang tre sang Day 3.
