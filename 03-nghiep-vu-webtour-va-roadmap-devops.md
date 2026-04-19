# WebTour - Tong Hop Nghiep Vu Cu, Nghiep Vu Moi Va Roadmap DevOps

## 1. Muc tieu tai lieu
Tai lieu nay tong hop toan bo nghiep vu WebTour theo 3 nhom:
- Nghiep vu da co trong project cu.
- Nghiep vu moi de nang cap gia tri san pham.
- Roadmap ky thuat + DevOps de trien khai theo tung giai doan.

## 2. Nghiep vu hien co (as-is)

### 2.1 Khach hang
- Dang ky/dang nhap tai khoan.
- Tim kiem tour, xem chi tiet tour.
- Dat tour va theo doi thong tin dat tour.
- Xem lich su booking.
- Danh gia, nhan xet dich vu.
- Thanh toan nhieu hinh thuc (tien mat/chuyen khoan/vi dien tu).
- Chat realtime voi nhan vien ho tro.

### 2.2 Quan tri vien/Nhan vien
- Quan ly CRUD tour.
- Quan ly khuyen mai theo tour.
- Quan ly danh sach booking.
- Quan ly danh sach danh gia.
- Quan ly nhan vien.
- Xem thong ke doanh thu va so booking.

## 3. Nghiep vu moi de phat trien (to-be)

### 3.1 Recommendation Engine
- Goi y tour theo hanh vi tim kiem, da xem, da dat.
- Uu tien tour co conversion cao theo phan khuc nguoi dung.
- Ky thuat: clickstream events + search/ranking service.

### 3.2 Loyalty & Membership
- Tich diem GoCoin theo gia tri don hang.
- Hang thanh vien Silver/Gold/Platinum.
- Doi diem lay voucher, uu dai.

### 3.3 Wishlist & Price Alert
- Luu tour yeu thich.
- Theo doi bien dong gia va so cho con lai.
- Gui push/email khi sap het cho hoac gia giam.

### 3.4 Social SSO
- Dang nhap mot cham bang Google/Facebook/Apple.
- Giam friction o buoc onboarding.

### 3.5 Dynamic Itinerary & Add-ons
- Them dich vu phu khi dat tour (dua don, bao hiem, nang cap phong).
- Tinh gia dong theo lua chon.

### 3.6 Flash Sale Campaign
- Ma giam gia gioi han theo thoi gian va so luong.
- Bat buoc co lock de tranh vuot quota.

## 4. Mapping nghiep vu -> service -> techstack

| Nghiep vu | Service chinh | Cong nghe de xuat |
|---|---|---|
| Dang nhap, phan quyen | Identity Service | Node.js, PostgreSQL/MongoDB, Redis, JWT/OAuth2 |
| CRUD tour/category/destination/promo/review | Core Service | Node.js, PostgreSQL + MongoDB |
| Tim kiem/filter tour | Search Service | Elasticsearch/OpenSearch, Redis |
| Dat tour va giu cho | Booking Service | PostgreSQL, Redis Lock, RabbitMQ/Kafka |
| Thanh toan | Payment Service | PostgreSQL, Gateway SDK, Retry + Circuit Breaker |
| Chat + ticket ho tro | Support Service | Socket.IO, MongoDB, queue worker |
| Tich diem/khuyen mai | Loyalty/Promotion Service | PostgreSQL, Redis lock/counter, Event bus |
| Goi y thong minh | Recommendation Service (pha sau) | Event stream, Elasticsearch, ranking pipeline |

## 5. Nghiệp vu trong tam can giai quyet bang techstack DevOps

### 5.1 Search bottleneck
- Van de:
  - Truy van DB truc tiep qua nhieu bo loc se cham khi traffic tang.
- Giai phap:
  - Tach Search read model o Elasticsearch.
  - Redis cache trang home/tour hot.
  - CDN cho static assets.

### 5.2 Concurrency overbooking
- Van de:
  - Nhieu user dat cung tour sap het cho.
- Giai phap:
  - Redis distributed lock + TTL reservation.
  - Booking transaction ACID o PostgreSQL.
  - Compensation flow neu payment fail.

### 5.3 Slow notification
- Van de:
  - Gui mail/SMS trong request sync lam UX cham.
- Giai phap:
  - Day tac vu thong bao vao queue.
  - Worker xu ly bat dong bo + retry + dead-letter queue.

### 5.4 Third-party payment instability
- Van de:
  - API vi dien tu timeout/gian doan.
- Giai phap:
  - Circuit breaker.
  - Timeout, exponential backoff retry.
  - Idempotency callback.

## 6. Roadmap trien khai theo giai doan

### Giai doan 0 - Khao sat va chuan hoa (1 tuan)
- Chot bounded context.
- Chot danh sach endpoint hien tai.
- Chot convention log, trace id, error response.

Deliverables:
- Context map.
- API inventory.
- Tech decision record (ADR).

### Giai doan 1 - Nen tang Microservices + DevOps (2 tuan)
- Dung API Gateway.
- Dockerize Identity va Core service dau tien.
- Tao CI pipeline (lint, test, build image).
- Setup metrics/log co ban.

Deliverables:
- Gateway running.
- 1-2 service deploy duoc bang container.
- CI action chay on push.

### Giai doan 2 - Tach Auth + Catalog (2-3 tuan)
- Tach login/role service rieng.
- Tach Core Service (catalog/promo/review) va Search Service rieng.
- Them Redis cache, Elasticsearch index.

Deliverables:
- Search latency giam ro rang.
- Auth route qua gateway.

### Giai doan 3 - Tach Booking + Payment + Queue (3-4 tuan)
- Dung PostgreSQL cho booking/payment.
- Trien khai event bus.
- Cai saga choreography va compensation.

Deliverables:
- Dat tour hoat dong theo event.
- Co test case payment fail -> booking cancel.

### Giai doan 4 - Support + Analytics (2 tuan)
- Tach support realtime (chat + ticket).
- Trien khai analytics pipeline va dashboard.

Deliverables:
- Response ho tro nhanh va co ticket lifecycle.
- Co dashboard KPI booking-payment.

### Giai doan 5 - Nghiep vu nang cao (3-5 tuan)
- Loyalty, wishlist, flash sale, recommendation.
- A/B test goi y tour.

Deliverables:
- Tang conversion va retention metrics.

## 7. DevOps stack de xuat cho do an
- Source control: GitHub.
- CI/CD: GitHub Actions.
- Container: Docker, Docker Compose (hoc ky do an) hoac Kubernetes (mo rong).
- Config: .env theo environment + secret manager co ban.
- Monitoring: Prometheus + Grafana.
- Log aggregation: Loki/ELK (neu co thoi gian).
- Tracing: OpenTelemetry + Jaeger.

## 8. KPI danh gia thanh cong
- P95 latency search < 300ms (co cache).
- Ty le booking thanh cong > 98% (khong tinh payment gateway downtime).
- Ty le overbooking = 0 cho flow da lock.
- Mean time to detect incident < 5 phut (co alert).
- Deployment frequency tang so voi monolith truoc do.

## 9. Backlog uu tien cho nhom
- P1:
  - API Gateway + Identity + Core + Search.
  - Docker Compose + CI can ban.
- P2:
  - Booking + Payment + Saga + Redis lock.
  - Monitoring dashboard.
- P3:
  - Support service (chat + ticket).
  - Loyalty, wishlist, recommendation.

## 10. Ghi chu de bao ve do an
- Trinh bay theo "problem -> architecture decision -> trade-off -> ket qua".
- Demo 2 tinh huong that bai:
  - Payment fail va compensation thanh cong.
  - Cong payment timeout nhung he thong khong sap day chuyen.
- Co sequence diagram va architecture diagram cho moi luong nghiep vu chinh.
