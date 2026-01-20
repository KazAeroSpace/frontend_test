---

# Тестовое задание

## Веб-картографическое приложение для мониторинга ДТП

### Цель задания

Разработать клиентское веб-приложение для визуализации и мониторинга **ДТП в городе Астана** с использованием **React** и картографической библиотеки.
Данные должны загружаться динамически по API ArcGIS REST.

Задание проверяет:

* архитектурное мышление,
* умение работать с картами и геосервисами,
* работу с большими наборами пространственных данных,
* производительность и качество кода.

---

## Технологии

**Обязательно:**

* React + TypeScript
* MobX — состояние UI и карты
* **SWR или React Query** — загрузка данных
* Любая карта: MapLibre GL / Mapbox GL / ArcGIS JS SDK

**По желанию:**

* Vite / Next.js
* Любой UI-фреймворк

---
## Исходные данные (API)

### 1. Точки ДТП (Point)

API GET для получения точек ДТП по Астане:

```
https://gis.kgp.kz/arcgis/rest/services/KPSSU/DTP/FeatureServer/0/query?where=area_code+%3D+%271971%27&objectIds=&time=&geometry=&geometryType=esriGeometryPoint&inSR=&spatialRel=esriSpatialRelIntersects&distance=&units=esriSRUnit_Foot&relationParam=&outFields=*&returnGeometry=true&maxAllowableOffset=&geometryPrecision=&outSR=4326&havingClause=&gdbVersion=&historicMoment=&returnDistinctValues=false&returnIdsOnly=false&returnCountOnly=false&returnExtentOnly=false&orderByFields=&groupByFieldsForStatistics=&outStatistics=&returnZ=false&returnM=false&multipatchOption=xyFootprint&resultOffset=&resultRecordCount=&returnTrueCurves=false&returnExceededLimitFeatures=false&quantizationParameters=&returnCentroid=false&timeReferenceUnknownClient=false&sqlFormat=none&resultType=&featureEncoding=esriDefault&datumTransformation=&f=geojson
```
Формат ответа: `GeoJSON (Point)`


---

### 2. Границы города Астана (MultiPolygon)

GET

```
https://services8.arcgis.com/GyR85gR88mMqIY4t/ArcGIS/rest/services/Open_dataset_of_administrative_boundaries_of_Kazakhstan_WFL1/FeatureServer/1/query?where=name_en%3D%27Astana%27&objectIds=&geometry=&geometryType=esriGeometryPolygon&inSR=&spatialRel=esriSpatialRelIntersects&resultType=none&distance=0.0&units=esriSRUnit_Meter&outDistance=&relationParam=&returnGeodetic=false&outFields=*&returnGeometry=true&returnCentroid=false&returnEnvelope=false&featureEncoding=esriDefault&multipatchOption=xyFootprint&maxAllowableOffset=&geometryPrecision=&outSR=4326&defaultSR=&datumTransformation=&applyVCSProjection=false&returnIdsOnly=false&returnUniqueIdsOnly=false&returnCountOnly=false&returnExtentOnly=false&returnQueryGeometry=false&returnDistinctValues=false&cacheHint=false&collation=&orderByFields=&groupByFieldsForStatistics=&returnAggIds=false&outStatistics=&having=&resultOffset=&resultRecordCount=&returnZ=false&returnM=false&returnTrueCurves=false&returnExceededLimitFeatures=true&quantizationParameters=&sqlFormat=none&f=pgeojson&token=
```

Формат ответа: `GeoJSON (MultiPolygon)`

## Функциональные требования

### 1. Карта

* Интерактивная карта.
* Центр — **Астана**.
* Подложка — OpenStreetMap или аналог.

---

### 2. Загрузка данных

* Загрузка ДТП по API.
* Использовать **SWR или React Query**:

  * кэширование,
  * refetch (кнопка или событие).
* MobX **не использовать для хранения данных API**.

---

### 3. Отображение объектов

* Точки ДТП отображаются на карте.
* Граница города Астана отображается полигоном.
* Разные стили для:

  * точек,
  * кластеров,
  * полигона.

---

### 4. Кластеризация

* Кластеризация точек ДТП.
* При клике на кластер — увеличение масштаба.
* Кастомный стиль кластера (цвет + количество).

---

### 5. Управление слоями

* Переключатели (on/off):

  * точки ДТП,
  * кластеры,
  * граница города.
* Состояние хранить в MobX.

---

### 6. Взаимодействие

* Клик по точке ДТП:

  * popup с информацией (ID, координаты, любые поля).
* Подсветка выбранной точки.

---

## Архитектура

* Чёткая структура проекта (feature-based / модульная).
* Разделение ответственности:

  * **React Query / SWR — данные**,
  * **MobX — UI и состояние карты**,
  * карта отдельно от UI.

---

## Результат

* GitHub-репозиторий.
* README с:
  * инструкцией запуска,
  * описанием архитектуры,
  * описанием работы с API.

---

## Критерии оценки

| Критерий        | Что смотрят                       |
| --------------- | --------------------------------- |
| Архитектура     | Понятная и расширяемая структура  |
| Работа с картой | Слои, кластеры, события           |
| Data fetching   | Корректное использование SWR / RQ |
| MobX            | Только UI и состояние карты       |
| TypeScript      | Типизация, аккуратность           |
| Code style      | Читаемость, нейминг               |
