# Member Onboarding and Conflict Playbook

## 1. Role map chinh thuc
- The Anh: Lead, gateway, infra, merge gate.
- Tuan Anh: Core + Search.
- Viet Cuong: Booking focus.
- Duc Hau: Payment + Support.

## 2. Cau tra loi mac dinh khi thanh vien vao chat
Neu thanh vien noi "toi la [ten], viec cua toi la gi?", tro ly phai:
1. Xac nhan ten trong role map.
2. Hoi Day hien tai (1..10).
3. Tra task P1 trong ngay do.
4. Tra input can lay tu nguoi khac.
5. Tra output phai nop 17h30.

## 3. Mapping task theo nguoi (rut gon)

### The Anh
- Chot architecture, conventions, event naming.
- Setup infra compose local.
- Gateway route, auth middleware, correlation id.
- Review merge gate, security hardening, release notes.

### Tuan Anh
- Core entities va CRUD.
- Search endpoint, filter/sort.
- Core->Search event publisher.
- Cache tuning va bugfix Core/Search.

### Viet Cuong
- Booking entities, status flow.
- Passenger, cancellation, reservation lock.
- Booking event publish/consume.
- Saga booking side + compensation + concurrent test.

### Duc Hau
- Payment entities, payment intent.
- Webhook verify signature, idempotency.
- Payment event publish/consume, refund.
- Support service ticket/chat API.

## 4. Rule anti-conflict code (bat buoc)
1. Contract lock:
- OpenAPI + event schema lock tu Day 1.
- Moi thay doi contract phai duoc The Anh approve.

2. File ownership lock theo service:
- Core/Search: Tuan Anh la owner.
- Booking: Viet Cuong la owner.
- Payment/Support: Duc Hau la owner.
- Gateway/infra/shared: The Anh la owner.

3. Branch strategy:
- Moi task 1 branch rieng: feature/dayX-service-task.
- Khong commit truc tiep len main.

4. Merge strategy:
- PR can 1 reviewer bat buoc.
- CI pass moi duoc merge.
- Sau 17h30 chi merge bugfix P1.

5. Schema/migration safety:
- Migration script phai backward-compatible trong sprint.
- Khong doi ten field critical neu chua co migration plan.

## 5. Nhip triage khi co conflict
- Buoc 1 (5 phut): xac dinh conflict o contract hay implementation.
- Buoc 2 (10 phut): owner service de xuat fix.
- Buoc 3 (10 phut): The Anh chot solution cuoi.
- Buoc 4 (5 phut): cap nhat docs va thong bao team.

## 6. Checklist tra loi nhanh cho thanh vien
Khi tra task trong ngay, bat buoc format:
1. Viec P1 hom nay.
2. Files/API duoc sua.
3. Input can lay.
4. Output phai nop.
5. Risk conflict va cach tranh.
