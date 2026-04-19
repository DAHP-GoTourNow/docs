# Booking Service - Thiet ke chi tiet

## 1. Vai tro
Booking Service xu ly transaction dat tour va trang thai don.

Muc tieu:
- Bao toan nhat quan don dat.
- Chong overbooking o thoi diem cao.
- Tach luong dat tour khoi Core catalog.

## 2. Chuc nang chinh
- Tao booking.
- Quan ly passenger.
- Them booking note.
- Huy booking theo policy.
- Quan ly reservation lock (TTL).
- Dong bo trang thai theo ket qua payment.

## 3. Model du lieu chinh
- bookings:
  - id, bookingCode, userId, tourId, departureId, status, priceSnapshot, promotionSnapshot, createdAt.
- passengers:
  - id, bookingId, fullName, dob, ageGroup, idCardNumber.
- booking_notes:
  - id, bookingId, content, createdAt.
- cancellations:
  - id, bookingId, reason, refundAmount, createdAt.
- reservation_locks:
  - id, userId, tourId, departureId, quantity, expiresAt, status.

## 4. Constraints quan trong
- booking.userId FK -> identity.user.
- booking.tourId FK -> core.tour.
- booking.departureId FK -> core.departure.
- quantity > 0.
- status in {pending, confirmed, cancelled}.
- bookingCode unique.

## 5. API de xuat
- POST /booking
- GET /booking/:id
- GET /booking?userId=
- POST /booking/:id/cancel
- POST /booking/:id/lock
- POST /booking/:id/confirm

## 6. Event contracts
- BookingCreated
- BookingConfirmed
- BookingCancelled
- ReservationExpired

Lang nghe event:
- PaymentSucceeded
- PaymentFailed

## 7. Techstack de xuat
- Node.js + NestJS.
- PostgreSQL cho transaction.
- Redis cho reservation lock TTL.
- RabbitMQ/Kafka cho saga choreography.

## 8. KPI
- Ty le overbooking = 0.
- p95 create booking < 400ms (khong tinh payment).
- Ty le booking orphan = 0.

## 9. Roadmap
- Tuan 1: model booking + passenger + cancel.
- Tuan 2: reservation lock TTL + expiry worker.
- Tuan 3: saga voi payment + compensation.
