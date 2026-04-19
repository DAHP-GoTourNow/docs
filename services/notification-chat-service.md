# Notification Chat Service - Thiet ke chi tiet

## 1. Vai tro
Phu trach giao tiep voi khach hang theo thoi gian thuc va theo su kien:
- Chat realtime customer-staff.
- Gui thong bao email, push, in-app.

Muc tieu:
- Khong lam cham luong booking chinh.
- Dam bao thong bao gui du va co kha nang retry.

## 2. Chuc nang chinh

### 2.1 Chat realtime
- Tao phong chat customer-staff.
- Gui/nhan tin nhan realtime.
- Danh dau da xem.
- Gan ticket ho tro voi booking.

### 2.2 Notification event-based
- Nhan event tu Core/Payment/Auth.
- Render template va gui kenh phu hop.
- Luu log ket qua gui.

### 2.3 Notification scheduling
- Nhac lich khoi hanh truoc N ngay.
- Nhac thanh toan con thieu.
- Price alert theo wishlist.

## 3. CRUD bat buoc
- CRUD Conversation.
- CRUD Message.
- CRUD Notification Template.
- CRUD Notification Job.
- CRUD Notification Log.
- CRUD User Notification Preference.

## 4. Model du lieu chinh
- conversations:
  - id, customerId, staffId, status, createdAt.
- messages:
  - id, conversationId, senderId, content, sentAt, readAt.
- notification_templates:
  - id, code, channel, subject, body, isActive.
- notification_jobs:
  - id, templateCode, receiverId, payload, scheduledAt, status.
- notification_logs:
  - id, jobId, channel, providerResponse, status, sentAt.
- notification_preferences:
  - userId, emailEnabled, pushEnabled, smsEnabled.

## 5. API de xuat
- POST /chat/conversations
- GET /chat/conversations/:id/messages
- POST /chat/messages
- POST /notifications/send
- POST /notifications/schedule
- PATCH /notifications/preferences/:userId

## 6. Event tieu bieu
- BookingConfirmed -> gui email xac nhan.
- PaymentFailed -> gui canh bao thanh toan loi.
- DepartureReminderDue -> gui nhac lich di.
- PriceDropped -> gui thong bao gia.

## 7. Techstack de xuat
- Node.js + Socket.IO.
- MongoDB cho chat va log thong bao.
- Redis + BullMQ cho queue va scheduler.
- SMTP provider hoac email API provider.
- Firebase/APNs neu can push mobile.

## 8. Reliability va anti-spam
- Retry policy theo tung kenh thong bao.
- Dead letter queue cho job loi nhieu lan.
- Rate limit gui thong bao theo user.
- Co co che unsubscribe theo loai noi dung.

## 9. KPI
- Ty le gui thong bao thanh cong > 98%.
- p95 do tre chat realtime < 150ms trong cung khu vuc.
- Ty le job retry qua 3 lan < 2%.

## 10. Roadmap
- Tuan 1: chat realtime can ban + luu lich su.
- Tuan 2: template notification + event consumer.
- Tuan 3: scheduler nhac lich + preference center.
