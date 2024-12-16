# KOOKDATA
## 교통사고 데이터를 활용하여 사용자 유형에 맞는 사고다발지역 정보를 제공하는 서비스

### overview

2022년 교통사고 사망자 감소대책에 따라 정부와 교통안전공단은 보행자 안전을 최우선으로 하는 교통환경을 구축하고자 다양한 정책을 추진하고 있습니다. 하지만 현재 제공되는 교통정보 서비스는 주로 차량 중심으로 이루어져 있으며, 보행자나 이륜차와 같은 다양한 사고 유형에 대한 정보는 부족한 상황입니다. 이를 해결하고자, 교통사고 데이터를 활용해 각 사용자 유형에 맞는 사고다발지역 정보를 제공하는 서비스를 개발했습니다. 이 서비스는 보행자와 이륜차 이용자에게 보다 안전한 경로와 위험 지역을 안내함으로써 사고를 예방하고, 더 안전한 교통 환경을 만드는 데 기여할 수 있습니다.

### <기여한 부분만 작성>

**[데이터 수집]**
- 공공데이터 포털
- 전국교통사고다발지역표준데이터 (2017~2020)
- 도로교통공단_자전거사고다발지역정보서비스 (2015~2020)
- 도로교통공단_보행자무단횡단사고다발지역정보서비스 (2015~2020)
- 도로교통공단_보행노인사고다발지역정보서비스 (2015~2020)
- 도로교통공단_스쿨존어린이사고다발지역정보서비스 (2015~2020)
- 한국산업안전보건공단_이륜차 사고다발구역 조회서비스 (2017-2019)

**[데이터 전처리]**

-> 공공데이터포털의 open API를 사용하여 데이터 수집 -> 수집한 데이터를 파싱하여 아래와 같은 형식의 csv 파일로 가공함

-> 년도, 시도시군구명, 지점명, 각 사고의 발생 건수, 사상자 수, 사망자수, 위도, 경도 열 추출

  ![전처리 후 데이터셋 예시](https://i.esdrop.com/d/f/roqIf5Zmhy/164fM93YQl.png)

**[데이터 입력 및 인덱싱]**
  
사고 다발지역 데이터

→ Elastic 에 전처리한 데이터 업로드 후 인덱싱

→ 사고 다발지역을 map에 나타내기 위해 위/경도 데이터 reindex

사용자 위치 데이터

→ 사용자가 웹 페이지에 접근할 때, 백엔드를 통해 Elastic에 위치 데이터 업로드

  ![인덱싱 후 데이터 mapping 예시](https://i.esdrop.com/d/f/roqIf5Zmhy/d0dN5QsvzC.png)

**[DashBoard]**

#### 인덱싱한 데이터로 Kibana 시각화 (사고다발구역 위치 맵)

  ![사고다발구역 위치 맵 Kibana 시각화](https://i.esdrop.com/d/f/roqIf5Zmhy/ZikwsK9Jv9.png)

-> 위도와 경도로 사고다발구역을 지도에 표시하고, 레이어를 나누어 사고를 종류별로 확인할 수 있도록 함 (시간 필터를 활용해 년도별 사고위치, 사고발생건수, 사상자수, 사망자수 정보 확인 가능)


#### 인덱싱한 데이터로 Kibana 시각화 (교통사고 현황 분석)

  ![교통사고 현황 분석 Kibana 시각화](https://i.esdrop.com/d/f/roqIf5Zmhy/wdO662dQ93.png)

-> 교통사고 현황을 그래프로 나타내 한눈에 보기 쉽게 시각화함 (연간 부문별 교통사고 발생률 및 비율, 전체 교통사고 현황 및 사고다발지역 확인 가능)
