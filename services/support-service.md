# Support Service - Thiet ke chi tiet

## 1. Vai tro
Support Service quan ly chat realtime va ticket ho tro sau ban.

Muc tieu:
- Tach nghiep vu support khoi booking flow.
- Dam bao ho tro khach hang lien tuc.
- Co ticket lifecycle ro rang cho staff.

## 2. Chuc nang chinh
- Tao conversation giua client va staff.
- Gui/nhan message realtime.
- Tao support ticket tu chat hoac form.
- Quan ly ticket status va phan loai.

## 3. Model du lieu chinh
- conversations:
  - id, clientId, staffId, createdAt, updatedAt.
- messages:
  - id, conversationId, senderId, content, sentAt.
- support_tickets:
  - id, userId, title, category, content, status, createdAt, updatedAt.

## 4. Constraints
- conversation 1-N message.
- user 1-N supportTicket.
- supportTicket.status in {open, in_progress, resolved, closed}.
- message.content not null.

## 5. API de xuat
- POST /support/conversations
- GET /support/conversations/:id/messages
- POST /support/messages
- POST /support/tickets
- PATCH /support/tickets/:id/status
- GET /support/tickets?userId=

## 6. Realtime va async
- Realtime chat qua Socket.IO.
- Ticket notification day qua queue khi can email/push.

## 7. Techstack de xuat
- Node.js + Socket.IO.
- MongoDB cho conversation/message.
- PostgreSQL hoac MongoDB cho ticket (chon 1 theo team).
- Redis pub/sub cho horizontal scale socket.

## 8. KPI
- p95 chat delivery < 200ms.
- Ty le ticket duoc first-response < SLA muc tieu.
- Ty le loi realtime reconnect < 2%.

## 9. Roadmap
- Tuan 1: conversation + message + pagination.
- Tuan 2: support ticket workflow.
- Tuan 3: SLA metrics + queue thong bao.
