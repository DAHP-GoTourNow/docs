# Day 05 - Search + Reservation Lock + Payment Status Checklist

## Muc tieu ngay
- Search endpoint chay voi filter/sort.
- Reservation lock Redis TTL hoat dong.
- Payment status mapping on dinh.

## Checklist theo nguoi

### The Anh
- [ ] Chuan hoa error format xuyen service.
- [ ] Kiem tra gateway truyen correlationId den search/booking/payment.
- [ ] Review PR lock va search.

### Tuan Anh
- [ ] Tao endpoint /search/tours.
- [ ] Ho tro filter: category, destination, date, price.
- [ ] Ho tro sort co ban.

### Viet Cuong
- [ ] Tao reservation lock voi Redis TTL.
- [ ] Gan lock vao flow tao booking.
- [ ] Xu ly timeout lock va release lock.

### Duc Hau
- [ ] Chuan hoa payment status mapping.
- [ ] Retry policy can ban cho call gateway payment.
- [ ] Log audit cho thay doi status payment.

## Deliverables bat buoc cuoi ngay
- [ ] Search endpoint tra ket qua dung voi 3 bo filter mau.
- [ ] Reservation lock tao va het han dung.
- [ ] Payment status thay doi dung theo callback.

## Gate check
- [ ] Khong co deadlock lock-key trong Redis.
- [ ] p95 search duoi muc noi bo dat ra.
