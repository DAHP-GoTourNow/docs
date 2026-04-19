# Core Service - Catalog Promotion Review (dong bo class diagram)

## 1. Muc tieu
Core Service trong ban moi chi tap trung vao:
- Catalog (Tour, Category, Destination, Departure, PriceConfig).
- Promotion.
- Review.

Booking da tach sang Booking Service.

## 2. Kien truc tong quan (ban hien tai)

### 2.1 Vi tri cua Core trong kien truc
Core nhan request qua API Gateway va giao tiep voi:
- Search Service (dong bo index/read model).
- Booking Service (tra cuu tour/departure/promo).
- Payment Service (qua Booking events).
- Support Service (ticket lien quan tour neu can).

### 2.2 Ly do boundary nay
- Cohesion cao cho domain read-heavy cua san pham tour.
- Tranh tron transaction dat tour vao cung service catalog.
- De scale doc-lon (catalog) va ghi-lon (booking) doc lap.

## 3. Module chinh trong Core

### 3.1 Chuc nang tong
Core Service chua cac module sau:
- Catalog module.
- Promotion module.
- Review and rating module.
- Master data module (Transportation, basic taxonomies).

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

#### C. Nhom Promotion
- CRUD Promotion.
- CRUD PromotionCondition.
- CRUD PromotionTarget (tour/departure/category).

#### D. Nhom Review
- CRUD Review.
- CRUD ReviewMedia.
- CRUD ReviewComment.
- CRUD ReviewModeration.

#### E. Nhom Master Data
- CRUD Transportation.
- CRUD TourTag (neu can).
- CRUD Region mapping.

### 3.3 Nghiep vu hien dai can co trong Core
- Dynamic pricing config theo departure/age group.
- Quan ly schedule departure va so luong toi da.
- Promotion theo khung thoi gian va dieu kien.
- Workflow review moderation va phan hoi.

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

### 4.3 Quan he booking tham chieu
- Booking Service tham chieu Tour va Departure qua FK.
- Booking luu gia snapshot, promotion snapshot tai thoi diem dat.

### 4.4 Quan he promotion va review
- 1 Tour co the thuoc nhieu Promotion.
- 1 Tour co nhieu Review.
- 1 Review co nhieu ReviewMedia va ReviewComment.

## 5. Service lien quan ngoai Core

### 5.1 API Gateway
- Routing.
- Rate limit.
- JWT pre-check.
- Request ID cho tracing.

### 5.2 Identity/Auth Service
- Dang ky/dang nhap.
- Role customer/staff/admin.
- JWT, refresh token, social login.

### 5.3 Search Service
- Nhan dong bo du lieu tour.
- Toi uu tim kiem va bo loc.
- Cache ket qua query read-heavy.

### 5.4 Booking Service
- Quan ly booking transaction.
- Passenger, cancellation, reservation lock.
- Saga voi Payment Service.

### 5.5 Payment Service
- Payment intent, webhook idempotent, refund.

### 5.6 Support Service
- Conversation, message, support ticket.

## 6. Techstack de xuat cho ban 1 Core Service

### 6.1 Backend va du lieu
- Node.js + NestJS.
- PostgreSQL cho catalog/promotion quan he.
- MongoDB cho review media/comment neu can linh hoat.
- Redis cho cache lookup.

### 6.2 Search va su kien
- Event bus de dong bo sang Search Service.
- Outbox pattern cho cap nhat index an toan.

### 6.3 Van hanh DevOps
- Docker Compose cho local va demo.
- GitHub Actions cho CI.
- Prometheus + Grafana cho monitoring.
- OpenTelemetry + Jaeger cho tracing.

## 7. Lo trinh thuc thi thuc te

### Pha 1
- Dung API Gateway + Identity + Core.
- Hoan thien CRUD TourCategory, Tour, Destination, Departure, PriceConfig.

### Pha 2
- Them Promotion va workflow Review.
- Dong bo index sang Search Service.

### Pha 3
- Tich hop Booking Service va Payment Service.
- Toi uu consistency va event contracts.

### Pha 4 (tach dan neu can)
- Recommendation va loyalty o pha nang cao.
- Toi uu analytics va governance.

## 8. Checklist day du cho website du lich hien dai
- Co danh muc tour day du va quan he tour ro rang.
- Co module departure va price config ro rang.
- Co promotion va review moderation.
- Co booking payment on dinh, chong overbooking.
- Co loyalty, flash sale, wishlist, price alert.
- Co dashboard quan tri va so lieu kinh doanh.
- Co monitoring, logging, tracing de van hanh.

