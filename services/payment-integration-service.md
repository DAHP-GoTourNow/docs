# Payment Integration Service - Thiet ke chi tiet

## 1. Vai tro
Xu ly toan bo nghiep vu thanh toan va doi soat voi cong thanh toan ben thu 3.

Muc tieu:
- Dam bao tinh dung dan va idempotency giao dich.
- Khoanh vung rui ro khi cong thanh toan bat on.
- Cung cap trang thai giao dich nhanh cho Core Service.

## 2. Chuc nang chinh
- Tao payment intent tu booking.
- Chuyen huong nguoi dung den cong thanh toan.
- Nhan webhook callback tu cong thanh toan.
- Xac minh chu ky callback.
- Cap nhat trang thai giao dich va phat event.
- Ho tro refund mot phan hoac toan phan.

## 3. CRUD bat buoc
- CRUD Payment Transaction.
- CRUD Payment Intent.
- CRUD Gateway Config.
- CRUD Webhook Delivery Log.
- CRUD Reconciliation Record.
- CRUD Refund Transaction.

## 4. Model du lieu chinh
- payment_intents:
  - intentId, bookingId, amount, currency, status, expiresAt.
- payment_transactions:
  - txId, intentId, gateway, gatewayTxId, status, paidAt.
- payment_webhook_logs:
  - id, gateway, signatureValid, payloadHash, receivedAt.
- payment_reconciliations:
  - id, date, totalGateway, totalInternal, diffAmount, status.
- refund_transactions:
  - refundId, txId, amount, reason, status.

## 5. API de xuat
- POST /payment/intents
- GET /payment/intents/:id
- POST /payment/webhooks/:gateway
- POST /payment/refunds
- GET /payment/transactions/:id
- GET /payment/reconciliation/daily

## 6. Event can phat
- PaymentPending.
- PaymentSucceeded.
- PaymentFailed.
- PaymentRefunded.

Event nay duoc Core Service lang nghe de doi trang thai booking.

## 7. Bao mat va reliability
- Bat buoc idempotency key cho create intent.
- Verify HMAC signature cua webhook.
- Retry voi exponential backoff.
- Circuit breaker khi gateway loi cao.
- Dead letter queue cho callback xu ly that bai.

## 8. Techstack de xuat
- Node.js + NestJS/Express.
- PostgreSQL.
- Redis cho idempotency cache.
- RabbitMQ cho event giao tiep noi bo.

## 9. KPI
- Ty le callback xu ly thanh cong > 99.5%.
- Ty le giao dich duplicate = 0.
- p95 create payment intent < 300ms.
- Reconciliation sai lech = 0 hoac duoi nguong cho phep.

## 10. Roadmap
- Tuan 1: payment intent + callback verification.
- Tuan 2: idempotency + retry + circuit breaker.
- Tuan 3: refund flow + reconciliation report.
