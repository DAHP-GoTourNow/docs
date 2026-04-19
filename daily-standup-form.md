# Daily Standup Form - WebTour BE (10-day Sprint)

## Cach dung nhanh
- Moi sang, moi thanh vien copy nguyen block mau ben duoi va dien trong 3-5 phut.
- Post len nhom truoc 9:00.
- Neu co blocker, danh dau [BLOCKER] de The Anh triage ngay.

## Mau chung (copy/paste)

### 1) Thong tin
- Ngay sprint: Day [1..10]
- Thanh vien: [The Anh / Tuan Anh / Viet Cuong / Duc Hau]
- Service phu trach hom nay: [Gateway/Identity/Core/Search/Booking/Payment/Support/Infra]

### 2) Hom qua da xong
- [ ] Task 1:
- [ ] Task 2:
- [ ] Task 3:

### 3) Hom nay P1 (toi da 3 task)
- [ ] P1.1:
- [ ] P1.2:
- [ ] P1.3:

### 4) Input can nhan tu nguoi khac
- Nguoi can phoi hop:
- Can gi (API/schema/event/data/test):
- Deadline can nhan:

### 5) Output bat buoc nop 17h30
- [ ] Code/PR:
- [ ] Test result:
- [ ] Doc/contract cap nhat:

### 6) Blocker va muc do
- [NONE / LOW / MEDIUM / HIGH]
- Mo ta blocker:
- [BLOCKER] Neu HIGH, can The Anh quyet trong <= 30 phut.

### 7) Risk conflict code
- Files/API se sua hom nay:
- Contract nao co nguy co xung dot:
- Cach tranh conflict (lock contract/rebase/chia file ownership):

### 8) Kiem tra chat luong truoc khi push
- [ ] Co correlationId trong log.
- [ ] Co test toi thieu cho luong chinh.
- [ ] Payload/response dung OpenAPI da chot.
- [ ] Khong doi contract ma khong thong bao.

---

## Mau rieng theo tung vai tro

### The Anh (Lead/Gateway/Infra)
- Uu tien: infra compose, gateway middleware, merge gate, release risk.
- Bat buoc bao cao:
  - Tinh trang route /auth /core /search /booking /payment /support.
  - Tinh trang CORS/rate-limit/security headers.
  - Danh sach PR cho merge gate hom nay.

### Tuan Anh (Core/Search)
- Uu tien: Core CRUD, Search endpoint, Core->Search event sync.
- Bat buoc bao cao:
  - Constraint schema (price/quantity/status).
  - Search latency va cache status.

### Viet Cuong (Booking Focus)
- Uu tien: booking flow, reservation lock, saga booking side.
- Bat buoc bao cao:
  - Ket qua test overbooking.
  - Ket qua compensation khi PaymentFailed.

### Duc Hau (Payment + Support)
- Uu tien: payment intent/webhook/idempotency, support ticket/chat.
- Bat buoc bao cao:
  - Ket qua callback duplicate.
  - Tinh trang support API pagination.

---

## Quy tac triage blocker (The Anh dieu phoi)
1. 9:00-9:15 doc nhanh standup cua ca team.
2. Blocker HIGH duoc triage trong <= 30 phut.
3. Neu blocker lien quan contract, chot owner va cap nhat docs ngay.
4. 17:30 doi chieu output bat buoc truoc khi sang ngay moi.