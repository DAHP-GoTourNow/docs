# WebTour - Kien truc 1 Core Service cho Website Du Lich Day Du

## 1. Muc tieu tai thiet ke
Tai lieu nay dieu chinh theo huong ban yeu cau: gom cac nghiep vu kinh doanh vao 1 Core Service de de lam va de quan tri trong do an, nhung van giu kha nang mo rong len microservices sau nay.

Muc tieu:
- Gom business logic vao 1 trung tam de phat trien nhanh.
- Liet ke day du CRUD con thieu cua website du lich hien dai.
- Mo ta ro quan he du lieu cua 1 tour va cac thanh phan lien quan.
- Van dat san cac diem neo de tach service o giai doan sau.

## 2. Kien truc tong quan (ban hien tai)

### 2.1 Service can co
1. API Gateway
2. Identity/Auth Service
3. Core Business Service
4. Payment Integration Service
5. Notification Chat Service
6. Analytics Reporting Service

Trong do, toan bo nghiep vu CRUD va nghiep vu van hanh website du lich se duoc dua vao Core Business Service.

### 2.2 Ly do gom thanh 1 Core Service
- Nhom do an de kiem soat pham vi va deadline.
- Tranh over-engineering qua som.
- Giam chi phi van hanh va debug.
- Co the tach dan theo module sau khi on dinh.

## 3. Core Business Service (trung tam)

### 3.1 Chuc nang tong
Core Business Service chua cac module sau:
- Catalog module.
- Booking module.
- Inventory module.
- Promotion and loyalty module.
- Content and news module.
- Review and rating module.
- Master data module.

### 3.2 Danh sach CRUD day du can co

#### A. Nhom Tour va danh muc
- CRUD Tour.
- CRUD Tour Type:
  - Du lich trong nuoc.
  - Du lich nuoc ngoai.
  - Du lich khach doan.
  - Du lich hanh huong.
- CRUD Tour Theme (bien, nui, van hoa, am thuc, trekking).
- CRUD Destination (quoc gia, tinh thanh, diem den).
- CRUD Itinerary (lich trinh theo ngay).
- CRUD Departure (lich khoi hanh, so cho, han dat).
- CRUD Tour Price Rule (gia theo mua, gia theo doi tuoi, phu thu phong don).
- CRUD Tour Add-on (bao hiem, dua don, nang cap dich vu).
- CRUD Hot Tour (flag hot, uu tien hien thi, khung thoi gian hot).

#### B. Nhom doi tac va tai nguyen
- CRUD Huong dan vien.
- CRUD Khach san.
- CRUD Hang phong khach san.
- CRUD Phuong tien di chuyen (xe, may bay, tau).
- CRUD Nha hang/diem an uong trong tour.

Luu y cho khach san:
- Bat buoc luu mapLink.
- Nen luu them lat, lng de tim quanh ban do va loc khoang cach.

#### C. Nhom Booking van hanh
- CRUD Booking.
- CRUD Passenger.
- CRUD Booking Item (tour + departure + gia tai thoi diem dat).
- CRUD Payment Reference (tham chieu den giao dich thanh toan).
- CRUD Booking Status History.
- CRUD Refund Request.

#### D. Nhom Marketing va cham soc khach hang
- CRUD Voucher/Coupon.
- CRUD Flash Sale Campaign.
- CRUD Loyalty Rule.
- CRUD Loyalty Wallet (GoCoin).
- CRUD Wishlist.
- CRUD Price Alert.
- CRUD Customer Review.

#### E. Nhom Noi dung va truyen thong
- CRUD Tin tuc (News).
- CRUD Danh muc tin tuc.
- CRUD Banner, Hero Section, Landing Block.
- CRUD FAQ.
- CRUD Policy page (hoan huy, thanh toan, bao mat).

### 3.3 Nghiep vu hien dai can co trong Core
- Dynamic pricing theo mua cao diem va so cho con lai.
- Gio hang tam cho dat tour nhieu lua chon.
- Giu cho tam thoi (reservation lock) khi cho thanh toan.
- Quan ly cho ngoi theo departure, tranh overbooking.
- Ghi nhan hanh vi xem tour de phuc vu recommendation sau nay.
- Khoi tao workflow duyet review va chong spam.

## 4. Quan he du lieu day du cua 1 tour

### 4.1 Quan he bat buoc
- 1 Tour thuoc 1 Tour Type.
- 1 Tour co nhieu Departure.
- 1 Tour co nhieu Itinerary Day.
- 1 Tour co nhieu Media Asset (anh, video).
- 1 Tour co nhieu Review.
- 1 Tour co nhieu Add-on.
- 1 Tour co the duoc gan nhieu Hot Tour campaign theo tung thoi diem.
- 1 Tour lien ket nhieu Destination theo thu tu hanh trinh.

### 4.2 Quan he doi tac van hanh
- 1 Departure co the gan 1 hoac nhieu Huong dan vien.
- 1 Departure co the gan nhieu Khach san theo tung dem.
- 1 Departure co the gan nhieu Phuong tien di chuyen.

### 4.3 Quan he dat tour
- 1 Booking co nhieu Passenger.
- 1 Booking co 1 hoac nhieu Booking Item.
- 1 Booking co 0..n Payment Transaction.
- 1 Booking co 0..n Refund Request.

### 4.4 Quan he marketing
- 1 Voucher ap dung cho nhieu Tour.
- 1 Tour co the thuoc nhieu campaign (flash sale, seasonal sale, hot tour).
- 1 User co 1 Loyalty Wallet va nhieu Loyalty Transaction.

## 5. Service con lai ngoai Core

### 5.1 API Gateway
- Routing.
- Rate limit.
- JWT pre-check.
- Request ID cho tracing.

### 5.2 Identity/Auth Service
- Dang ky/dang nhap.
- Role customer/staff/admin.
- JWT, refresh token, social login.

### 5.3 Payment Integration Service
- Tao payment intent.
- Webhook callback.
- Idempotency key.
- Retry va circuit breaker khi cong thanh toan loi.

### 5.4 Notification Chat Service
- Chat realtime customer-staff.
- Gui email booking, nhac lich khoi hanh, thong bao gia.
- Push notification cho wishlist va flash sale.

### 5.5 Analytics Reporting Service
- Doanh thu theo ngay, theo tour, theo kenh.
- Conversion funnel (search -> detail -> booking -> payment).
- Dashboard cho admin.

## 6. Techstack de xuat cho ban 1 Core Service

### 6.1 Backend va du lieu
- Node.js + NestJS (de quan ly module lon trong 1 service).
- PostgreSQL cho transaction va quan he phuc tap.
- MongoDB cho content mem deo (news, chat archive neu can).
- Redis cho cache, lock, queue state.

### 6.2 Search va xu ly su kien
- Elasticsearch/OpenSearch cho search tour.
- RabbitMQ cho event noi bo (notification, loyalty update).

### 6.3 Van hanh DevOps
- Docker Compose cho local va demo.
- GitHub Actions cho CI.
- Prometheus + Grafana cho monitoring.
- OpenTelemetry + Jaeger cho tracing.

## 7. Lo trinh thuc thi thuc te

### Pha 1
- Dung API Gateway + Auth + Core Service.
- Hoan thien CRUD bat buoc: tour, loai tour, huong dan vien, khach san, tin tuc.

### Pha 2
- Them booking, reservation lock, payment callback.
- Them hot tour, coupon, loyalty can ban.

### Pha 3
- Them search nang cao, recommendation can ban, analytics dashboard.
- Toi uu hieu nang va bo sung canh bao he thong.

### Pha 4 (tach dan neu can)
- Tach Booking thanh service rieng.
- Tach Promotion/Loyalty thanh service rieng.
- Tach Catalog Search thanh service rieng.

## 8. Checklist day du cho website du lich hien dai
- Co danh muc tour day du va quan he tour ro rang.
- Co module huong dan vien, khach san, phuong tien.
- Co module tin tuc va noi dung marketing.
- Co booking payment on dinh, chong overbooking.
- Co loyalty, flash sale, wishlist, price alert.
- Co dashboard quan tri va so lieu kinh doanh.
- Co monitoring, logging, tracing de van hanh.

