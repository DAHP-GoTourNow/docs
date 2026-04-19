# WebTour V2 BE - Roadmap 10 ngay V2 (da toi uu tai va giam bottleneck)

## 1. Team va vai tro (ban chot)

| Nhan su | Vai tro | Trach nhiem chinh |
|---|---|---|
| The Anh | Dev chinh / Tech lead | Architecture, Gateway, infra compose, review gate, release control |
| Tuan Anh | Dev phu 1 | Core Service + Search + data model |
| Viet Cuong | Dev phu 2 | Booking Service (tap trung 100%) |
| Duc Hau | Dev bank payment | Payment Service + Support Service |

Quy tac:
- Moi task co 1 owner ro rang.
- PR bat buoc 1 reviewer.
- Khong merge neu chua dat DoD.

## 2. Scope BE trong 10 ngay
Lam du trong 10 ngay:
- API Gateway
- Identity Service (co ban)
- Core Service (Catalog, Promotion, Review)
- Search Service
- Booking Service
- Payment Service
- Support Service (ticket + chat API)

De sau 10 ngay:
- Analytics nang cao
- Loyalty, wishlist, recommendation

## 3. Chien luoc bat buoc de khong vo plan
1. Day 1 chot Mock API JSON (Postman/collection) cho Core, Booking, Payment de code song song.
2. Day 1-2 The Anh setup infra full local: Redis + Message Broker + DB + search.
3. Day 4-5 pub/sub event mock truoc khi rap saga that.
4. Day 7 rap Saga, Day 8 chi test edge cases va concurrent load.

## 4. Muc tieu tung ngay

| Ngay | Muc tieu |
|---|---|
| Day 1 | Freeze schema, constraints, OpenAPI, event contracts, Mock API JSON |
| Day 2 | Dung skeleton service + Gateway + full infra local compose |
| Day 3 | Identity + Core CRUD can ban + Payment intent can ban |
| Day 4 | Core CRUD day du + Booking logic co ban + webhook verify |
| Day 5 | Search + Reservation lock + payment status mapping |
| Day 6 | Event integration lien service (Core/Search + Booking/Payment) |
| Day 7 | Rap Saga booking-payment (confirm/cancel/compensation co ban) |
| Day 8 | Test concurrent + edge case + callback duplicate |
| Day 9 | Support service + hardening + E2E regression |
| Day 10 | Bugfix P1/P2 + UAT + Release Candidate + docs freeze |

## 5. Bang phan cong chi tiet theo ngay (V2)

| Ngay | The Anh (Lead/Gateway/Infra) | Tuan Anh (Core/Search) | Viet Cuong (Booking Focus) | Duc Hau (Payment + Support) |
|---|---|---|---|---|
| Day 1 | Chot architecture, OpenAPI conventions, event naming, Mock API format | Chot Core entities + response mock | Chot Booking entities + response mock | Chot Payment entities + callback payload |
| Day 2 | Setup docker compose: gateway, redis, broker, db, search | Khoi tao Core service + migration schema | Khoi tao Booking service + migration schema | Khoi tao Payment service + adapter mock |
| Day 3 | Identity login/register/refresh + JWT + auth middleware | Core CRUD Category, Destination | Booking CRUD co ban (khong doi Core xong nhờ mock) | Payment intent API + transaction table |
| Day 4 | Review merge + route wiring qua gateway | Core CRUD Tour, Departure, PriceConfig | Booking status machine + validation | Webhook verify signature + idempotency key |
| Day 5 | Chuan hoa error format + traceId xuyen service | Search endpoint /search/tours + filter/sort | Passenger + reservation lock Redis TTL | Payment status mapping + retry policy can ban |
| Day 6 | Tich hop gateway -> tat ca service + smoke test | Event publisher Core->Search (TourUpdated) | Pub BookingCreated event | Consume BookingCreated + PaymentSucceeded/Failed event |
| Day 7 | Hardening CORS/rate-limit + review saga PR | Search cache Redis + query tuning | Rap Saga phia Booking: confirm/cancel theo payment | Rap Saga phia Payment: publish success/fail + refund API |
| Day 8 | To chuc test E2E va unblock nhanh | Ho tro promotion/review endpoint can ban | Test concurrent overbooking + compensation flow | Test callback duplicate + reconciliation log |
| Day 9 | RC checklist + security review | Bugfix Core/Search P1 | Bugfix Booking P1 + log cleanup | Lam Support Service: ticket + chat API + pagination |
| Day 10 | Final merge gate, release notes, docs freeze | Bugfix P2 + UAT support | Bugfix P2 + UAT support | Bugfix Payment/Support + go-live checklist |

## 6. Task backlog theo service (owner ro rang)

| Service | Task | Owner | Reviewer | Priority | DoD |
|---|---|---|---|---|---|
| Infra | Docker compose Redis + Broker + DB + Search | The Anh | Duc Hau | P1 | 1 lenh run local thanh cong cho team |
| API Gateway | Route + auth pre-check + traceId | The Anh | Viet Cuong | P1 | Tat ca route service di qua gateway |
| Identity | register/login/refresh/logout | The Anh | Duc Hau | P1 | JWT flow chay, test auth pass |
| Core | CRUD Category, Tour, Destination, Departure, PriceConfig | Tuan Anh | The Anh | P1 | CRUD + validation + index DB |
| Search | /search/tours + sync event + cache | Tuan Anh | The Anh | P1 | Tim kiem + filter + sort pass |
| Booking | Booking, Passenger, Cancellation, status flow | Viet Cuong | The Anh | P1 | Khong orphan, status dung |
| Booking | Reservation lock Redis TTL + concurrent test | Viet Cuong | Duc Hau | P1 | Test tai cao khong overbooking |
| Payment | payment intent + webhook verify + idempotency | Duc Hau | The Anh | P1 | Callback duplicate khong tao giao dich moi |
| Payment | refund + reconciliation log co ban | Duc Hau | Viet Cuong | P2 | Co audit du lieu giao dich |
| Support | ticket + chat API + pagination | Duc Hau | Tuan Anh | P2 | API chay, pagination dung |

## 7. Dependency quan trong
1. Booking confirm phu thuoc Payment callback.
2. Search sync phu thuoc Core event publisher.
3. Tat ca FE-BE integration phu thuoc Gateway route on dinh.
4. Reservation lock va Saga phu thuoc Redis + Broker setup tu Day 2.
5. Booking va Payment code song song duoc nho Mock API da chot Day 1.

## 8. Definition of Done (bat buoc)
- Co code chay duoc local compose.
- Co test toi thieu cho luong chinh.
- Co log dung format + traceId.
- Co cap nhat API contract neu doi payload.
- PR duoc review va CI pass.
- Docs cap nhat sau merge.

## 9. Nhip van hanh 10 ngay
- Daily 9h: standup 15 phut (focus blocker).
- Daily 17h30: triage bug/blocker va chot scope ngay sau.
- Day 5: demo giua ky (bat buoc).
- Day 7: checkpoint saga (bat buoc pass smoke test).
- Day 9: freeze feature, chi bugfix.
- Day 10: UAT + release candidate.

## 10. Risk cao va cach xu ly nhanh

| Risk | Owner xu ly | Cach xu ly nhanh |
|---|---|---|
| Viet Cuong bi qua tai Booking | The Anh | Khong giao Support cho Viet Cuong, giu booking focus |
| Duc Hau nhe tai sau Day 5 | The Anh | Chuyen Support service sang Duc Hau |
| Saga rap tre gay vo plan | The Anh + Viet Cuong + Duc Hau | Rap Saga Day 7, Day 8 chi edge-case test |
| Blocker do service phu thuoc nhau | Tat ca | Dung Mock API JSON tu Day 1 |
| Message broker/Redis setup tre | The Anh | Setup full infra ngay Day 1-2 |

## 11. Tieu chi hoan thanh sau 10 ngay
- Dang nhap va auth flow chay.
- CRUD tour co ban chay qua gateway.
- Search hoat dong voi filter/sort/cache co ban.
- Booking-Payment chay end-to-end co saga co ban.
- Khong overbooking trong test concurrent.
- Support ticket/chat API co ban chay.
- Docs va contracts dong bo voi implementation.

## 12. Pro-tips thuc chien (ap dung bat buoc)
1. Postman Mock Server:
- Day 1, The Anh import OpenAPI vao Postman va bat Mock Server co URL that.
- Cac service goi URL mock nhu service that de code song song.

2. Docker Compose Hybrid local:
- Compose chi chua backing services: PostgreSQL, MongoDB, Redis, Broker, Elasticsearch.
- Code service chay tren host (localhost) de debug nhanh, hot-reload nhanh.

3. TraceId/CorrelationId tu Gateway:
- Day 2 tao middleware sinh X-Correlation-ID (UUID).
- Gateway truyen header nay xuong tat ca service.
- Moi service bat buoc ghi log kem correlationId.

## 13. Daily Checklist files (10 file)
- Day 1: docs/daily-checklists/day-01-design-freeze.md
- Day 2: docs/daily-checklists/day-02-skeleton-infra.md
- Day 3: docs/daily-checklists/day-03-auth-core-payment-base.md
- Day 4: docs/daily-checklists/day-04-core-booking-webhook.md
- Day 5: docs/daily-checklists/day-05-search-lock-status.md
- Day 6: docs/daily-checklists/day-06-event-integration.md
- Day 7: docs/daily-checklists/day-07-saga-assembly.md
- Day 8: docs/daily-checklists/day-08-edgecase-loadtest.md
- Day 9: docs/daily-checklists/day-09-support-hardening.md
- Day 10: docs/daily-checklists/day-10-uat-release.md
