# Day 10 - UAT + Release Candidate Checklist

## Muc tieu ngay
- Chot bugfix cuoi.
- Chay UAT voi frontend.
- Dong bang docs/contracts va tao release candidate.

## Checklist theo nguoi

### The Anh
- [ ] Final merge gate cho tat ca PR con lai.
- [ ] Tao release notes backend v2.
- [ ] Chot runbook rollback neu gap su co demo.

### Tuan Anh
- [ ] Fix toan bo bug Core/Search con mo.
- [ ] Verify search filter/sort/cache trong UAT.
- [ ] Chot docs service Core/Search.

### Viet Cuong
- [ ] Fix bug Booking/Saga con mo.
- [ ] Verify overbooking test lan cuoi.
- [ ] Chot docs service Booking va checklist compensation.

### Duc Hau
- [ ] Fix bug Payment/Support con mo.
- [ ] Verify webhook idempotency lan cuoi.
- [ ] Chot go-live checklist cho payment callback.

## UAT checklist bat buoc
- [ ] Login lay token va goi API protected thanh cong.
- [ ] CRUD tour co ban qua gateway.
- [ ] Search filter/sort tra ket qua dung.
- [ ] Booking -> payment success -> confirmed.
- [ ] Booking -> payment fail -> cancelled + unlock.
- [ ] Support ticket/chat API hoat dong.

## Deliverables bat buoc cuoi ngay
- [ ] Release Candidate backend v2.
- [ ] Danh sach bug con lai (neu co) kem muc do va owner.
- [ ] Docs/contracts da freeze va dong bo.

## Gate check
- [ ] Bug P1 = 0 truoc khi chot RC.
- [ ] Team dong y release readiness.
