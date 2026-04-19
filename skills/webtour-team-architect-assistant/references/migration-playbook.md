# Migration Playbook - WebTour

## 1. Nguyen ly xuong tay
- Khong dap di xay lai.
- Ap dung Strangler Fig: gateway dung truoc, route dan sang service moi.
- Chia boundary theo nghiep vu dang ton tai trong code.
- Moi service so huu du lieu rieng.
- Booking-Payment-Notification chuyen sang event-driven.

## 2. Boundary de xuat cho team
1. API Gateway.
2. Identity Service.
3. Core Service (Catalog, Promotion, Review).
4. Search Service.
5. Booking Service.
6. Payment Service.
7. Support Service (Chat + Ticket).

Analytics Reporting la pha sau va khong nam trong boundary v1 cua class diagram moi.

## 3. Lo trinh theo pha

### Pha 0
- Inventory hien trang API/model.
- Chot contract va convention log/trace.

### Pha 1
- Dat Gateway.
- Tach Auth.
- Chuyen frontend goi qua gateway.

### Pha 2
- Refactor Catalog bo N+1 va chuan hoa model tour/category/destination/departure.
- Tach Search service.

### Pha 3
- Tach Booking service.
- Xay Payment service + idempotency.
- Them reservation lock Redis + TTL va saga booking-payment.

### Pha 4
- Tach Support service (chat + ticket).
- Trien khai analytics reporting (pha sau).
- Bo sung loyalty, wishlist, recommendation.

## 4. KPI/DoD can dat
- Search p95 latency duoi muc muc tieu da dat.
- Ty le overbooking = 0 trong flow moi.
- Payment callback khong duplicate transaction.
- Dashboard co metric request, error, latency.
- CI/CD chay duoc build-test-deploy.
