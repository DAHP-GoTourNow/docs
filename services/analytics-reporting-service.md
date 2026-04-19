# Analytics Reporting Service - Thiet ke chi tiet

## 1. Vai tro
Tong hop du lieu va cung cap bao cao dieu hanh cho admin va staff.

Muc tieu:
- Do luong hieu qua kinh doanh theo thoi gian thuc gan-thoi-gian-thuc.
- Ho tro quyet dinh gia, campaign, san pham tour.

## 2. Chuc nang chinh
- Dashboard doanh thu tong quan.
- Bao cao booking theo ngay/tuan/thang.
- Bao cao theo kenh (web, mobile, campaign).
- Bao cao hieu qua tour, destination, huong dan vien.
- Funnel conversion:
  - search -> view detail -> add booking -> payment success.

## 3. CRUD bat buoc
- CRUD Dashboard Widget Config.
- CRUD Report Template.
- CRUD Report Schedule.
- CRUD KPI Definition.
- CRUD Alert Rule.

## 4. Nguon du lieu
- Event tu Core Service:
  - TourViewed, BookingCreated, BookingCancelled.
- Event tu Payment Service:
  - PaymentSucceeded, PaymentFailed, PaymentRefunded.
- Event tu Auth Service:
  - UserRegistered, UserLoggedIn.

## 5. Model du lieu phan tich
- fact_bookings.
- fact_payments.
- fact_user_activity.
- dim_tour.
- dim_destination.
- dim_time.

Co the dung data mart don gian trong PostgreSQL giai doan dau.

## 6. API de xuat
- GET /analytics/dashboard/overview
- GET /analytics/revenue
- GET /analytics/bookings
- GET /analytics/conversion-funnel
- POST /analytics/reports/export
- POST /analytics/alerts

## 7. Cac bao cao bat buoc cho website du lich
- Doanh thu theo loai tour:
  - trong nuoc, nuoc ngoai, khach doan, hanh huong.
- Top hot tour theo booking va doanh thu.
- Ty le huy tour theo departure.
- Ty le thanh toan thanh cong theo cong thanh toan.
- CAC, conversion rate, repeat booking rate.

## 8. Techstack de xuat
- Node.js + NestJS.
- PostgreSQL (OLAP nho o muc do an).
- Redis cache cho dashboard query nang.
- RabbitMQ consumer de nap event.
- Grafana cho visual dashboard nhanh.

## 9. KPI cua chinh service
- Do tre cap nhat dashboard < 5 phut.
- p95 query dashboard < 500ms voi du lieu tong hop.
- Ty le job aggregate loi < 1%.

## 10. Roadmap
- Tuan 1: thu thap event va fact table can ban.
- Tuan 2: dashboard doanh thu + booking.
- Tuan 3: funnel conversion + canh bao KPI.
