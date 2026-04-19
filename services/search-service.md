# Search Service - Deprecated boundary

## 1. Trang thai
Tai lieu nay duoc giu lai de tranh dut link cu.

Search khong con la service doc lap trong v1.
Search da duoc dua vao trong Core Service duoi dang Search and Discovery module.

## 2. Tai lieu thay the
- Thiet ke tong Core: docs/services/core-service.md
- Architecture index: docs/01-chia-service-microservices.md
- Roadmap nghiep vu: docs/03-nghiep-vu-webtour-va-roadmap-devops.md

## 3. Rule tuong thich endpoint
- Gateway van co the expose path /search/*.
- Backend handler map vao Core Service Search module.
- Neu can doi endpoint noi bo, uu tien /core/search/* de ro boundary.
