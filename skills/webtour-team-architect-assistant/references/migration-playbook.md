# Migration Playbook - WebTour

## 1. Nguyen ly xuong tay
- Khong dap di xay lai.
- Ap dung Strangler Fig: gateway dung truoc, route dan sang service moi.
- Chia boundary theo nghiep vu dang ton tai trong code.
- Moi service so huu du lieu rieng.
- Booking-Payment-Notification chuyen sang event-driven.

## 2. Boundary de xuat cho team
1. API Gateway.
2. Identity Auth Service.
3. Core Service.
4. Payment Integration Service.
5. Notification Chat Service.
6. Analytics Reporting Service.

Core Service la tam trong giai doan dau de giam do phuc tap delivery.

## 3. Lo trinh theo pha

### Pha 0
- Inventory hien trang API/model.
- Chot contract va convention log/trace.

### Pha 1
- Dat Gateway.
- Tach Auth.
- Chuyen frontend goi qua gateway.

### Pha 2
- Refactor Catalog bo N+1.
- Chuan hoa model tour/departure.

### Pha 3
- Xay Payment service.
- Them reservation lock Redis + TTL.
- Dung saga booking-payment.

### Pha 4
- Tach chat/notification jobs.
- Tach analytics reporting.
- Bo sung loyalty, wishlist, recommendation.

## 4. KPI/DoD can dat
- Search p95 latency duoi muc muc tieu da dat.
- Ty le overbooking = 0 trong flow moi.
- Payment callback khong duplicate transaction.
- Dashboard co metric request, error, latency.
- CI/CD chay duoc build-test-deploy.
