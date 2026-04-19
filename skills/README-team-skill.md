# Huong dan dung AI skill cho team WebTour

## 1. File skill da tao
- Skill source: docs/skills/webtour-team-architect-assistant/
- Skill package de chia se: docs/skills/dist/webtour-team-architect-assistant.skill

## 2. Muc dich skill
Skill nay giup dong nghiep:
- Phan tich hien trang he thong dua tren code/docs hien co.
- Tu van chia service va migration roadmap.
- Tao backlog ky thuat cho tung vai tro trong team.
- Chi ra gap thieu cua web du lich hien dai.
- Giao task theo ten thanh vien + theo ngay trong roadmap.
- Giam conflict code khi nhieu nguoi code song song.

## 3. Prompt mau cho team

### Prompt mo dau cho thanh vien moi
"Toi la [The Anh/Tuan Anh/Viet Cuong/Duc Hau], hom nay Day [1..10], hay giao viec P1 cho toi va output phai nop 17h30."

### Prompt khi bi block
"Toi la [ten], Day [x], toi dang block o [mo ta]. Hay chi ro input can lay tu ai va cach unblock trong 30 phut."

### Prompt de tranh conflict
"Toi sap sua [service/file]. Hay cho toi file ownership, contract lock va merge rule de tranh conflict code."

### Prompt 1 - Khao sat hien trang
"Phan tich hien trang WebTour tu code hien tai, chi ra bottleneck chinh va uu tien xu ly trong 2 tuan toi."

### Prompt 2 - Task breakdown
"Tu roadmap migration hien tai, lap backlog P1/P2/P3 cho Backend, Frontend, DevOps, QA."

### Prompt 3 - Service boundary
"Review boundary cua Core Service va de xuat neu can tach them Booking service trong pha tiep theo."

### Prompt 4 - Bao ve do an
"Tao script trinh bay 10 phut theo cau truc: van de, quyet dinh kien truc, trade-off, ket qua."

## 4. Prompt nhanh theo tung vai tro

### The Anh
"Toi la The Anh, Day [x]. Hay dua checklist lead trong ngay: infra/gateway/review gate/release gate."

### Tuan Anh
"Toi la Tuan Anh, Day [x]. Hay giao viec Core/Search theo uu tien P1 va output test can nop."

### Viet Cuong
"Toi la Viet Cuong, Day [x]. Hay giao viec Booking focus va cach test overbooking/saga."

### Duc Hau
"Toi la Duc Hau, Day [x]. Hay giao viec Payment + Support va checklist webhook idempotency."

## 5. Nguyen tac dung trong team
- Luon yeu cau co bang chung file khi ket luan ve hien trang.
- Khong chap nhan de xuat phat minh endpoint/model khong co trong code.
- Uu tien de xuat co the lam duoc trong pham vi do an.
- Khi giao viec phai co 5 muc: task, input can lay, output bat buoc, risk conflict, cach giam conflict.
