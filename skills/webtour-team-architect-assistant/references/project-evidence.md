# Project Evidence - WebTour as-is

Tai lieu nay tong hop bang chung hien trang tu code cu de skill tra loi dung boi canh.

## 1. Kien truc hien tai
- Backend dang la monolith Express.
- Dung 1 ket noi MongoDB dung chung cho nhieu module.
- Frontend goi truc tiep API base URL monolith.

Bang chung:
- backend_webtour/src/config/server.js
- backend_webtour/src/config/mongodb.js
- WebTour/src/apiServer.js

## 2. Models dang ton tai
- Account, User.
- Tour, Destination, TourImage, TourPackage.
- Booking, BookingDetail.
- Hotel.
- Chat.
- Contact.

Bang chung:
- backend_webtour/src/config/models/

## 3. Router va flow da co
- authRoutes: dang ky, dang nhap, doi mat khau.
- listTourRoutes: danh sach tour, search/filter, tour detail, favourite.
- bookingRoutes: tao booking, huy booking, thong ke.
- chatRoutes: socket chat va truy van tin nhan.
- customerRoutes, userRoutes: quan tri nguoi dung.

Bang chung:
- backend_webtour/src/config/routers/

## 4. Diem nghen ky thuat da xac nhan
- Search co nguy co N+1 query khi map qua tour image va destination.
- Booking tao Booking va BookingDetail theo kieu save tuan tu, chua thay transaction atomic.
- Chua thay inventory lock de chong overbooking.
- Account/User tach roi co nguy co lech du lieu khi update.
- Chat luu messages dang array lon, kho pagination theo quy mo.

## 5. Nang luc da co
- Auth co ban.
- Tour catalog/search co ban.
- Booking co ban.
- Chat realtime.
- Quan tri user/customer.
- Thong ke doanh thu co ban.

## 6. Muc con thieu cho web du lich hien dai
- Payment gateway thuc te + callback idempotency.
- Reservation lock + inventory theo departure.
- Notification async email/push/sms.
- Review/rating workflow day du.
- Loyalty, voucher, flash sale.
- Wishlist, price alert, recommendation.
- Observability va CI/CD day du.
