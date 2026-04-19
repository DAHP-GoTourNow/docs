

## Danh sach service hien tai
- core-service: [docs/services/core-service.md](docs/services/core-service.md)
- API Gateway: [docs/services/api-gateway-service.md](docs/services/api-gateway-service.md)
- Identity Auth: [docs/services/identity-auth-service.md](docs/services/identity-auth-service.md)
- Payment Integration: [docs/services/payment-integration-service.md](docs/services/payment-integration-service.md)
- Notification Chat: [docs/services/notification-chat-service.md](docs/services/notification-chat-service.md)
- Analytics Reporting: [docs/services/analytics-reporting-service.md](docs/services/analytics-reporting-service.md)
# Tong quan tai lieu chia service

## Nguyen ly de team doc nhanh
- Chia theo nghiep vu, khong chia theo bang du lieu.
- Moi du lieu co 1 service so huu.
- Uu tien tach module co tai cao/rui ro cao truoc.
- Sync cho request can ket qua ngay, async cho side-effect.
- Co metric, log, trace ngay tu dau de debug lien service.

# Nguyen ly chia service cho WebTour

## 1. Muc dich tai lieu
Tai lieu nay giup ca team thong nhat cach chia service de:
- De code, de test, de van hanh.
- Tranh chia sai boundary dan den phuc tap hon monolith.
- Co tieu chi ro rang de ra quyet dinh.

## 2. Nguyen ly cot loi

### 2.1 Chia theo business capability
- Moi service dai dien cho 1 nhom nghiep vu ro rang.
- Khong chia theo tang ky thuat (controller/service/repository).

Dung:
- Core Service quan ly tour, booking, inventory, content.

Khong dung:
- Tach service chi vi bang du lieu lon hoac vi team muon tach cho "dep".

### 2.2 Single ownership du lieu
- Moi du lieu chi co 1 service so huu va ghi chinh.
- Service khac muon dung du lieu thi qua API hoac event.

Quy tac:
- Cam query truc tiep DB service khac.

### 2.3 Cohesion cao, coupling thap
- Logic cung mot nghiep vu dat gan nhau.
- Phu thuoc giua service la toi thieu va co contract ro.

Tieu chi nhan biet chia dung:
- Team co the deploy service do doc lap.
- Loi service A khong lam sap service B.

### 2.4 Dat uu tien theo gia tri nghiep vu
- Tach truoc service co tai cao hoac rui ro cao:
  - Payment integration.
  - Notification chat.
  - Analytics.

### 2.5 Stateless va idempotent
- Service khong giu state session trong RAM local.
- Endpoint quan trong can idempotency:
  - Tao payment intent.
  - Webhook callback.
  - Booking confirm.

### 2.6 Sync cho query, async cho side-effect
- Sync: can response ngay (doc chi tiet tour, tao booking).
- Async: tac vu hau xu ly (gui email, cap nhat loyalty, analytics).

### 2.7 Version contract tu dau
- API versioning (/v1) va event versioning.
- Khong pha vo backward compatibility khong co ke hoach.

### 2.8 Observability la bat buoc
- Moi request co correlationId.
- Co metric, log, trace de debug lien service.

## 3. Tieu chi quyet dinh khi nao tach khoi Core Service
Chi tach module khoi Core khi dat it nhat 2 trong 4 tieu chi:
1. Team can release module do nhanh hon phan con lai.
2. Tai nguyen module do tang manh va can scale rieng.
3. Rui ro loi module do cao, can fault isolation.
4. Module co cong nghe dac thu (vi du search, ML recommendation).

## 4. Mau ap dung cho WebTour

### Hien tai
- Core Service la trung tam de tang toc do delivery.
- Service ben ngoai Core:
  - API Gateway.
  - Identity Auth.
  - Payment Integration.
  - Notification Chat.
  - Analytics Reporting.

### Sau nay (tach dan)
- Tach Booking Service rieng khi peak booking cao.
- Tach Promotion Loyalty khi campaign thay doi lien tuc.
- Tach Catalog Search khi truy van full-text qua lon.

## 5. Anti-pattern can tranh
- Shared database cho nhieu service.
- Service chat qua chat (call chain qua dai).
- Tach service qua nho ngay tu dau (nano-services).
- Khong co ownership ro rang, ai cung sua duoc.

## 6. Checklist review truoc khi chot boundary
- Boundary co map truc tiep toi nghiep vu khong?
- Ownership du lieu co ro rang khong?
- API contract da ro input output error chua?
- Co metric de theo doi rieng service chua?
- Co rollback plan neu tach that bai khong?

## 7. One-page summary cho dong nghiep
- Chia theo nghiep vu, khong chia theo bang.
- Moi du lieu co 1 chu so huu.
- Uu tien tach module co tai cao/rui ro cao.
- Sync cho luong can ngay, async cho side-effect.
- Co metric log trace tu ngay dau.
- Tach dan theo giai doan, khong dap di xay lai.
