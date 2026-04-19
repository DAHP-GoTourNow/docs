# Team Delivery Templates

## 1. Mau bao cao nhanh cho daily sync

1. Hien trang:
   - Da xong:
   - Dang lam:
   - Bi chan:
2. Tac dong toi migration:
   - ...
3. Ho tro can tu team:
   - ...

## 2. Mau gap analysis

1. As-is:
   - ...
2. Gap:
   - ...
3. To-be:
   - ...
4. DoD:
   - ...

## 3. Mau backlog ky thuat

| Epic | Task | Owner | Priority | Dependency | DoD |
|---|---|---|---|---|---|
| Gateway | Dat route v1 | Backend | P1 | None | Route auth/core qua gateway |
| Booking | Them reservation lock | Backend | P1 | Redis | Khong overbooking trong test concurrent |
| Payment | Webhook idempotency | Backend | P1 | Payment provider sandbox | Callback duplicate khong tao giao dich moi |
| Notification | Queue email | Backend | P2 | RabbitMQ | Gui mail async co retry |
| Observability | Dashboard latency | DevOps | P2 | Prometheus/Grafana | Co chart p95 va error rate |

## 4. Mau review architecture decision

1. Van de:
2. Lua chon:
3. Trade-off:
4. Quyet dinh:
5. Ke hoach rollback:
