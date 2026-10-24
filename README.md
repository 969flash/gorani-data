# Gorani data packs

Regional SQLite packs (xz-compressed) used by the [Gorani](https://969flash.github.io/gorani/) plugin for Rhino, Blender and SketchUp.
The plugin downloads only the packs that cover the site the user picks, when the user starts that action.

- Each release holds the packs of one folder: `data` (Korean parcel packs + `manifest.json`), `data/jp`, `data/nl`, `data/fr`, `data/ch`, `data/us`
  (large folders continue in `data/nl-2`, `data/us-2`, …). Each `manifest.json` lists the packs with their sha256 and bounds.
- Free to download, no account or key. The data comes from public open data; sources and licenses are listed below.
- Korean building, road and contour packs are not here. They are derived from the national base map, which Korean law (Spatial Data Act, Article 16)
  does not allow to be stored outside Korea, so they are served from a server in Korea. The manifest points to it.

---


Rhino 플러그인 Gorani가 대상지 주변만 받아 쓰는 지역 단위 SQLite 팩(xz 압축)입니다.

## 한국 — 시군구 팩 (좌표계 EPSG:5186)

- `<시군구코드>_site.db.xz` — 필지(토지특성정보 도형·속성), 토지이용계획 지정 현황, 계획 도형(서울 UPIS / 그 외 지정 코드로 필지를 합친 것)
- `manifest.json` — 팩 목록·sha256·범위. 플러그인이 읽는다.
- 건물·도로·수계·등고선 팩(`*_context`·`*_terrain`)은 여기 두지 않는다. 수치지형도(기본측량성과)에서 나온 자료라 국외 서버에 둘 수 없어
  (공간정보관리법 제16조) 국내 서버에 있고, 매니페스트에 그 주소가 적혀 있다.

출처·라이선스 (원천 그대로 — 가공: 재투영·병합·단순화·시군구 분할)
- 국토교통부 토지특성정보·토지이용계획정보 — 이용허락범위 제한 없음(공공데이터포털 15048121·15045900)
- 서울특별시 도시계획정보(UPIS) — 공공누리 제1유형
- 본 데이터는 정보제공 목적이며 법적 효력이 없다(국토교통부 국가중점데이터 안내).

## 일본 — 시구정촌 건물 팩 (`jp/`, 경위도) / 日本 — 市区町村の建物パック

- `jp/jp<시구정촌코드>_context.db.xz` — 국토교통성 3D 도시모델(PLATEAU)의 건물만: LOD0 외곽, LOD1 실측 높이(measuredHeight), 층수, 용도 코드. 306개 시구정촌, 도시마다 최신 연도판.
- `jp/manifest.json` — 일본 팩 목록·sha256·범위(경위도 [서, 남, 동, 북]).
- 각 팩의 `data_sources` 표에 도시 이름·연도·데이터셋 주소가 있다. 도시 경계의 3차 메시는 이웃 도시 팩에도 들어 있어 같은 건물이 두 팩에 있을 수 있다(gml:id로 걸러 낸다).

出典：3D都市モデル（Project PLATEAU）各市区町村（各年度）、国土交通省。CC BY 4.0（公共データ利用規約 第1.0版と互換）。著作権は各地方公共団体にあります。
加工：Gorani が建物の外形・高さ・階数・用途コードだけを抽出し、経緯度（小数6桁）に変換して市区町村ごとの SQLite にしました。国土交通省・地方公共団体が作成したものではありません。

## 네덜란드 — 도엽 건물 팩 (`nl/`, 경위도) / Nederland — gebouwen per kaartblad

- `nl/nl<도엽>_context.db.xz` — Kadaster 3D Basisvoorziening(hoogtestatistieken_gebouwen)의 건물 바닥 윤곽·높이(지붕 50 % − 지반)·건축연도·지붕형만. `nl/manifest.json`.
- Bron: Kadaster, 3D Basisvoorziening (CC BY 4.0, https://creativecommons.org/licenses/by/4.0/deed.nl), bewerkt door Gorani — alleen omtrek, hoogte, bouwjaar en daktype, omgezet naar WGS84 (6 decimalen).

## 프랑스 — 데파르트망 건물 팩 (`fr/`, 경위도) / France — bâtiments par département

- `fr/fr<데파르트망>_context.db.xz` — IGN BD TOPO® `batiment`의 바닥 윤곽·높이(hauteur, 처마)·층수·용도·출현일만(본토·코르시카). `fr/manifest.json`.
- Source : IGN, BD TOPO® (Licence Ouverte / Open Licence 2.0, Etalab), traité par Gorani — emprise, hauteur, étages, usage et date d'apparition uniquement, reprojetés en WGS84 (6 décimales).

## 스위스 — 1:25k 도엽 건물 팩 (`ch/`, 경위도) / Schweiz — Gebäude pro Kartenblatt

- `ch/ch<도엽>_context.db.xz` — swisstopo swissBUILDINGS3D 3.0 Beta의 바닥 윤곽(Floor)·높이(GESAMTHOEHE 또는 DACH_MAX − 지반)·종류·용도만(리히텐슈타인 포함). `ch/manifest.json`.
- Quelle: ©swisstopo, swissBUILDINGS3D 3.0 Beta (OGD-Nutzungsbedingungen — freie Nutzung und Weitergabe mit Quellenangabe), bearbeitet durch Gorani — nur Grundriss, Höhe, Objektart und Nutzung, umgerechnet nach WGS84 (6 Dezimalstellen).

## 미국 — 카운티 건물 팩 (`us/`, 경위도) / United States — buildings per county

- `us/us<카운티 FIPS 5자리>_context.db.xz` — Overture Maps Foundation buildings 테마(Microsoft ML Buildings·OpenStreetMap·Esri Community Maps 합본)의 바닥 윤곽·높이·층수·용도·이름만. 높이는 대부분 Microsoft ML 추정값이다(실측 아님). 카운티 경계는 미국 인구조사국 cartographic boundary(공개). `us/manifest.json`.
- Source: Overture Maps Foundation (buildings theme, release in each pack's `data_sources`), © OpenStreetMap contributors, Microsoft (Global ML Building Footprints) — **Open Database License (ODbL) 1.0**. The `us/` packs are derivative databases and are themselves made available under ODbL 1.0. Processed by Gorani: footprint, height, floors, class and name only, 6-decimal WGS84, split by county. Heights are mostly machine-learning estimates.
