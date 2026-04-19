# Tong quan tai lieu chia service (Dong bo voi class diagram moi)

## 1. Scope dong bo
Tai lieu nay da duoc dong bo theo:
- class diagram: docs/diagrams/class_diagram.txt
- architecture xml: docs/diagrams/kien_truc_he_thong.xml

Muc tieu:
- Mot nguon su that cho toan bo docs.
- Khong mau thuan giua diagram va service docs.

## 2. Kien truc service hien tai (v1)
1. API Gateway
2. Identity Service
3. Core Service (Catalog, Promotion, Review, Search)
4. Booking Service
5. Payment Service
6. Support Service (Chat va Ticket)

Thanh phan ha tang chung:
- Redis Cache (inventory lock, search cache)
- Event Bus (Kafka/RabbitMQ)

## 3. Quy tac data model da chot
- PK: _id (ObjectId) hoac UUID neu can giao tiep lien service.
- FK phai hien thi ro tren field.
- Dat ten field theo camelCase.
- Date luu Date object (ISO), khong luu string.
- price la Decimal/Number, co check > 0.
- quantity la Number, co check >= 0.
- status dung enum ro rang.

## 4. Quan he nghiep vu da chot
- User 1-N Booking.
- Tour 1-N Booking.
- Booking 1-1 Payment.
- Category 1-N Tour.
- Booking N-1 Departure (tham chieu lich khoi hanh).
- Conversation 1-N Message.

## 5. Danh sach tai lieu service (da dong bo)
- API Gateway: docs/services/api-gateway-service.md
- Identity Auth: docs/services/identity-auth-service.md
- Core Service: docs/services/core-service.md
- Booking Service: docs/services/booking-service.md
- Payment Integration: docs/services/payment-integration-service.md
- Support Service: docs/services/support-service.md

Luu y chuyen doi:
- Search khong tach service rieng trong v1.
- Tai lieu cu docs/services/search-service.md duoc giu lai de redirect va tranh dut link.

Tai lieu bo sung (pha sau, chua nam trong boundary v1 cua diagram moi):
- Analytics Reporting: docs/services/analytics-reporting-service.md
- Notification Chat (legacy naming): docs/services/notification-chat-service.md

## 6. Tai lieu migration va roadmap
- Nguyen ly migration: docs/02-nguyen-ly-chuyen-mvc-sang-microservices.md
- Nghiep vu va roadmap DevOps: docs/03-nghiep-vu-webtour-va-roadmap-devops.md

## 7. Checklist dong bo docs moi lan cap nhat diagram
- Cap nhat architecture index (file nay).
- Cap nhat boundary trong migration doc.
- Cap nhat mapping nghiep vu-service-techstack.
- Cap nhat service docs moi hoac doi ten service.
- Dam bao khong con doc nao goi sai ten service.
