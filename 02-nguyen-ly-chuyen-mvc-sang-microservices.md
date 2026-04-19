# WebTour - Nguyen Ly Chuyen Tu MVC Monolithic Sang Microservices (Duoc rut ra tu code hien tai)

## 1. Muc tieu tai lieu
Tai lieu nay duoc viet dua tren viec doc code cu, de:
- Mo ta dung hien trang he thong dang co.
- Chi ra diem nghen ky thuat va nghiep vu con thieu.
- Dua ra nguyen ly chuyen doi co co so, khong ly thuyet chung.

## 2. Hien trang he thong (as-is) tu code cu

### 2.1 Kien truc hien tai
- Backend dang la 1 monolith Express + MongoDB chung.
- Tat ca router chay cung 1 server va 1 ket noi DB.
- Frontend goi truc tiep API monolith qua mot base URL co dinh.

Bang chung file:
- backend_webtour/src/config/server.js
- backend_webtour/src/config/mongodb.js
- WebTour/src/apiServer.js

### 2.2 Model dang co
He thong da co cac model chinh:
- Account, User (auth va profile tach roi).
- Tour, Destination, TourImage, TourPackage.
- Booking, BookingDetail.
- Hotel.
- Chat.
- Contact.

Bang chung file:
- backend_webtour/src/config/models/Account.js
- backend_webtour/src/config/models/User.js
- backend_webtour/src/config/models/Tour.js
- backend_webtour/src/config/models/Booking.js
- backend_webtour/src/config/models/BookingDetail.js
- backend_webtour/src/config/models/Chat.js

### 2.3 API dang co
He thong da co cac router:
- authRoutes: dang nhap, dang ky, doi mat khau.
- listTourRoutes: danh sach tour, search/filter, favourite.
- bookingRoutes: tao booking, huy booking, thong ke doanh thu.
- chatRoutes: chat realtime voi Socket.IO.
- customerRoutes, userRoutes: quan tri user/customer.

Bang chung file:
- backend_webtour/src/config/routers/authRoutes.js
- backend_webtour/src/config/routers/listTourRoutes.js
- backend_webtour/src/config/routers/bookingRoutes.js
- backend_webtour/src/config/routers/chatRoutes.js

## 3. Van de ky thuat quan trong phat hien tu code

### 3.1 N+1 query o search tour
Trong list tour/search, moi tour lai query them TourImage va Destination -> do tre tang manh khi so tour lon.

Bang chung:
- backend_webtour/src/config/routers/listTourRoutes.js

### 3.2 Booking chua co transaction atomic
Flow tao Booking va BookingDetail dang save tuan tu, neu loi giua chung se de du lieu mo coi.

Bang chung:
- backend_webtour/src/config/routers/bookingRoutes.js

### 3.3 Chua co inventory lock, co nguy co overbooking
Chua thay co che giu cho tam thoi theo seat/departure.

Bang chung:
- backend_webtour/src/config/routers/bookingRoutes.js
- backend_webtour/src/config/models/Booking.js

### 3.4 Auth coupling va du lieu tach roi
Account va User tach rieng, update/deletion co the lech du lieu neu 1 ben loi.

Bang chung:
- backend_webtour/src/config/models/Account.js
- backend_webtour/src/config/models/User.js
- backend_webtour/src/config/routers/userRoutes.js

### 3.5 Chat luu message dang array lon
Message nam trong 1 document lon, kho phan trang va kho mo rong khi so tin nhan tang.

Bang chung:
- backend_webtour/src/config/models/Chat.js
- backend_webtour/src/config/routers/chatRoutes.js

## 4. Nghiep vu da co va nghiep vu con thieu

### 4.1 Da co
- Dang ky/dang nhap co ban.
- Xem tour, tim kiem tour.
- Dat tour co ban.
- Chat realtime.
- Quan tri user/customer.
- Thong ke doanh thu co ban.

### 4.2 Con thieu cho mot website tour hien dai
- Payment integration thuc te (MoMo, ZaloPay, VNPay, Stripe).
- Reservation lock va inventory theo departure.
- Notification email/push/sms theo su kien booking/payment.
- Review va rating day du.
- Loyalty, voucher, flash sale.
- Wishlist, price alert, recommendation.
- API contract versioning, tracing, idempotency, DLQ.

## 5. Nguyen ly chuyen doi (rut ra tu hien trang WebTour)

### 5.1 Khong viet lai toan bo, ap dung Strangler Fig
- Dat API Gateway phia truoc monolith.
- Endpoint nao tach xong thi route sang service moi.
- Endpoint nao chua tach thi van route ve monolith.

Ly do:
- Giam rui ro downtime.
- Team co the release theo dot nho.

### 5.2 Chot boundary theo nghiep vu that su dang co
- Boundary ban dau:
  - Identity Auth Service.
  - Core Service (catalog + booking + content + promotion can ban).
  - Payment Integration Service.
  - Notification Chat Service.
  - Analytics Reporting Service.

Ly do:
- Dung voi module dang ton tai trong code, de tach dan khong vo flow cu.

### 5.3 Database ownership ro rang
- Moi service so huu schema/collection cua minh.
- Cam query truc tiep DB cua service khac.
- Du lieu cheo di qua API hoac event bus.

### 5.4 Doi luong nhay cam sang async + idempotent
- Booking-Payment-Notification phai event-driven.
- Callback payment phai idempotency key.
- Booking thay doi trang thai theo saga events.

### 5.5 Uu tien sua bottleneck truoc khi scale
- Sua N+1 query trong Catalog.
- Them reservation lock trong Booking.
- Tach Auth som de on dinh bao mat va role.

## 6. Ban do chuyen doi tu code cu sang dich vu moi

### 6.1 Identity Auth Service
Di chuyen:
- Account.js, User.js.
- authRoutes.js + phan user auth quan ly.

Them moi bat buoc:
- JWT + refresh token lifecycle.
- Login rate limit.
- Password policy + reset flow chuan.

### 6.2 Core Service
Di chuyen:
- Tour, Destination, TourImage, TourPackage.
- Booking, BookingDetail.
- Contact va module content.

Them moi bat buoc:
- CRUD loai tour, huong dan vien, khach san mapLink.
- Inventory theo departure, reservation TTL.
- Tour relation day du (itinerary, add-on, hot tour).

### 6.3 Payment Integration Service (moi)
Them moi bat buoc:
- Tao payment intent.
- Webhook verify signature.
- Reconciliation va refund flow.
- Event PaymentSucceeded, PaymentFailed.

### 6.4 Notification Chat Service
Di chuyen:
- Chat.js + chatRoutes.js.

Them moi bat buoc:
- Message pagination.
- Notification template + retry queue.
- Email/push theo su kien booking va payment.

### 6.5 Analytics Reporting Service
Di chuyen:
- Endpoint thong ke tu bookingRoutes.

Them moi bat buoc:
- Funnel search -> detail -> booking -> payment.
- Dashboard KPI cho admin.
- Alert rule theo error rate va conversion drop.

## 7. Lo trinh chuyen doi de xai duoc ngay

### Pha 0 - Khoa hien trang va chuan hoa contract
- Freeze endpoint catalog hien tai.
- Lap inventory API/model hien co.
- Them requestId correlation cho log.

### Pha 1 - Gateway + Auth
- Dat API Gateway truoc monolith.
- Tach Auth service dau tien.
- Chuyen frontend sang goi qua gateway.

### Pha 2 - Catalog va Core Booking can ban
- Refactor search bo N+1.
- Chuan hoa model tour/departure.
- Gioi han booking flow theo schema moi.

### Pha 3 - Payment + Reservation lock
- Them payment service.
- Them Redis lock/TTL giu cho.
- Dung saga cho booking-payment.

### Pha 4 - Chat Notification + Analytics + nang cao
- Tach chat + notification jobs.
- Tach analytics pipeline.
- Bo sung loyalty, review, wishlist, recommendation.

## 8. Danh sach bo sung bat buoc (gap closure checklist)
- Co Payment service thuc te va callback idempotent.
- Co inventory lock chong overbooking.
- Co review/rating va moderation.
- Co notification async (email/push).
- Co loyalty-voucher-flash sale.
- Co observability (metrics, logs, tracing).
- Co CI/CD va regression test cho flow booking-payment.

## 9. Tieu chi done cho qua trinh migration
- Tat ca request frontend di qua Gateway, khong goi truc tiep monolith.
- Auth, Core, Payment, Notification, Analytics deploy doc lap.
- Booking khong con tao du lieu mo coi va khong overbooking.
- Payment callback khong tao duplicate transaction.
- Co dashboard p95 latency, error rate, booking success rate.
