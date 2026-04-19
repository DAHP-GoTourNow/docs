# Search Service - Thiet ke chi tiet

## 1. Vai tro
Search Service phuc vu toan bo query tim kiem va bo loc tour read-heavy.

Muc tieu:
- Cat giam tai truy van tu Core.
- Giam do tre tim kiem khi traffic cao.
- Ho tro full-text + filter nang cao.

## 2. Chuc nang chinh
- Tim kiem tour theo tu khoa.
- Filter theo category, destination, departure, gia, region.
- Sort theo gia, do pho bien, ngay khoi hanh.
- Suggest keyword va destination.

## 3. Du lieu va ownership
Search Service khong so huu write model goc.
- Write model goc o Core Service.
- Search index duoc dong bo qua event.

Read model chinh:
- tours_search:
  - tourId, title, category, destinations, nextDeparture, minPrice, isHot, status.

## 4. Event contracts
- Core phat event:
  - TourCreated
  - TourUpdated
  - TourDeleted
  - DepartureUpdated
  - PromotionUpdated

Search xu ly event de cap nhat index eventual consistency.

## 5. API de xuat
- GET /search/tours?q=&category=&destination=&fromDate=&toDate=&minPrice=&maxPrice=&page=&size=
- GET /search/suggestions?q=
- GET /search/destinations?q=

## 6. Techstack de xuat
- Elasticsearch/OpenSearch.
- Redis cache ket qua query hot.
- RabbitMQ/Kafka consumer cho event sync.

## 7. KPI
- p95 latency search < 300ms.
- Search error rate < 1%.
- Index lag (event -> searchable) < 60s.

## 8. Roadmap
- Tuan 1: tao index + schema + endpoint can ban.
- Tuan 2: event consumer dong bo tu Core.
- Tuan 3: cache + query tuning + observability.
