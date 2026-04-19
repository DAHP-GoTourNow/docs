# API Gateway Service - Thiet ke chi tiet

## 1. Vai tro
API Gateway la cua vao duy nhat cho tat ca client:
- Web khach hang.
- Trang quan tri admin/staff.
- App mobile (neu mo rong sau).

Muc tieu:
- Dinh tuyen request den dung service phia sau.
- Chuan hoa bao mat va chinh sach truy cap.
- Quan sat he thong theo request id thong nhat.

## 2. Pham vi chuc nang

### 2.1 Routing va service discovery
- Route theo path prefix:
  - /auth -> Identity Service.
  - /core -> Core Service.
  - /search -> Core Service (Search module).
  - /booking -> Booking Service.
  - /payment -> Payment Service.
  - /support -> Support Service.
  - /analytics -> Analytics Service (pha sau).
- Ho tro versioning endpoint:
  - /api/v1/...

### 2.2 Bao mat
- JWT pre-check o tang gateway.
- RBAC co ban theo role customer/staff/admin.
- CORS policy theo whitelist domain.
- IP allowlist cho endpoint nhay cam (admin/internal).

### 2.3 Traffic governance
- Rate limit theo IP, user id, API key.
- Request size limit va body validation can ban.
- Timeout, retry policy va fallback response.

### 2.4 Observability
- Gan requestId/correlationId cho moi request.
- Access log, error log co cau truc JSON.
- Export metric: RPS, p95 latency, 4xx/5xx rate.

## 3. Du lieu cau hinh can quan ly (CRUD)
- CRUD Route Rule.
- CRUD Rate Limit Policy.
- CRUD CORS Policy.
- CRUD API Consumer (neu co API key ben doi tac).
- CRUD Circuit Breaker Rule cho downstream.

## 4. API endpoint quan tri gateway (goi y)
- POST /gateway/routes
- GET /gateway/routes
- PATCH /gateway/routes/:id
- DELETE /gateway/routes/:id
- POST /gateway/policies/rate-limit
- GET /gateway/health

## 5. Luong nghiep vu mau

### Dang nhap
1. Client goi /api/v1/auth/login vao gateway.
2. Gateway validate schema co ban.
3. Gateway route den Auth Service.
4. Tra response ve client kem correlationId.

### Dat tour
1. Client goi /api/v1/booking.
2. Gateway check JWT + role.
3. Gateway route sang Booking Service.
4. Neu payment callback, gateway route sang Payment Service theo webhook path.

## 6. Techstack de xuat
- Nginx hoac Kong.
- Redis cho distributed rate limit counter.
- OpenTelemetry collector.
- Prometheus exporter.

## 7. Non-functional requirements
- Do tre them boi gateway < 20ms.
- Uptime >= 99.9%.
- Ho tro horizontal scaling stateless.
- Co rolling update khong downtime.

## 8. Bao mat can bat buoc
- Chan request khong co user-agent hop le (co chinh sach).
- Header security: X-Content-Type-Options, X-Frame-Options.
- Gioi han endpoint auth de giam brute-force.
- An payload nhay cam trong log.

## 9. KPI quan tri
- p95 latency theo tung route.
- Ty le 401/403.
- Ty le 429 (rate limited).
- Ty le loi downstream theo tung service.

## 10. Roadmap trien khai
- Tuan 1: routing + JWT pre-check + CORS.
- Tuan 2: rate limit + correlationId + dashboard metric.
- Tuan 3: canary route + chinh sach retry/timeout.
