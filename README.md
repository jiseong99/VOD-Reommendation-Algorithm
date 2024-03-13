# VOD-Reommendation-Algorithm
## HelloPick! VOD 추천 웹서비스 프로젝트 / LG 헬로비전 Final Project


<br/>

## 1. 크롤링
#### VOD 컨텐츠 포스터 크롤링

![image](https://github.com/jiseong99/VOD-Reommendation-Algorithm/assets/137580822/37a989bf-2b7e-4789-a50c-9125a7986dc1)


+ 영화 데이터베이스 사이트인 TMDB에서 Selenium을 활용, 포스터 크롤링 진행

<br/>

## 2. 추천시스템 모델링
#### 협업 필터링

+ 협업 필터링은 user, item, grade 컬럼이 필요 -> grade 와 관련된 컬럼이 주어진 데이터에 존재하지 않음
+ grade 관련 파생 변수 생성
+ (해당 사용자가 특정 컨텐츠를 시청한 시간) / ( 특정 컨텐츠의 총 컨텐츠 길이) = (시청률) 이라는 파생 변수 생성
+ 해당 파생변수를 grade 대신 사용

![image](https://github.com/jiseong99/VOD-Reommendation-Algorithm/assets/137580822/fbaea191-c85b-4b08-aa71-22329e3555d2)

<br/>

+ Surprise 라이브러리 활용
+ ALS, SGD, KNNWithMeans, KNNBaseline, SVD, SVDpp, NMF 모델 사용 / precision@k가 가장 높은 모델을 사용할 예정

![image](https://github.com/jiseong99/VOD-Reommendation-Algorithm/assets/137580822/47b0b3ef-9788-4b20-ad29-91d86b608df2)

+ SVDpp 모델의 precision@10 이 0.042 정도로 제일 높음ㅁ

<br/>

#### precision@k 가 낮게 나온 원인
+ grade 대신에 사용한 '시청률' 이라는 파생변수가 평점을 충분히 대표하지 못했기에 precision@k가 낮게 나왔다고 판단함
+ 관련 논문 참고시 평점 관련 컬럼이 없는 경우 다양한 컬럼들을 바탕으로 평점 컬럼을 재정의한 경우가 대다수임

<br/>

#### grade 관련 함수 정의 / 추가 파생변수 생성
+ time_weight 변수는 최근 본 컨텐츠에 대해 더 가중치를 주는 지표 / 가장 최근 날짜 기준으로 1부터 지수평활법을 활용하여 과거로 갈수록 감소됨.
+ subsr_series_interest : 해당 사용자가 특정 시리즈에 대하여 해당 시리즈물을 몇 회차나 봤는지 보여주는 지표 : (사용자가 시청한 해당  시리즈의  회차 개수) / ( 해당 시리즈의 전체 회차 개수)
+ popular_all : 많이 시청된 컨텐츠에 가중치를 주는 지표 : (해당 컨텐츠를 시청한 사용자 수) / (전체 사용자 수)
+ series_count_asset_normalized : 해당 시리즈에 회차가 몇개나 있는지를 정규화한 변수, 정규화 방식 : origin / max
+ subsr_count_asset_normalized : 변수는 사용자가 컨텐츠를 몇 개나 시청하였는지를 정규화한 변수 , 정규화 방식 : origin / max
  
![image](https://github.com/jiseong99/VOD-Reommendation-Algorithm/assets/137580822/d9faf958-4793-4de8-b0f7-b01d004f195e)


<br/>

