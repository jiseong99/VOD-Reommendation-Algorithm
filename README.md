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

+ 협업 필터링은 user, item, grade 컬럼이 필요 -> grade 와 관련된 컬럼이 존재하지 않음
+ grade 관련 파생 변수 생성
+ (해당 사용자가 특정 컨텐츠를 시청한 시간) / ( 특정 컨텐츠의 총 컨텐츠 길이) = (시청률) 이라는 파생 변수 생성
+ 해당 파생변수를 grade 대신 사용

![image](https://github.com/jiseong99/VOD-Reommendation-Algorithm/assets/137580822/fbaea191-c85b-4b08-aa71-22329e3555d2)

<br/>

+ Surprise 라이브러리 활용
+ ALS, SGD, KNNWithMeans, KNNBaseline, SVD, SVDpp, NMF 모델 사용 / precision@k가 가장 높은 모델을 사용할 예정

![image](https://github.com/jiseong99/VOD-Reommendation-Algorithm/assets/137580822/47b0b3ef-9788-4b20-ad29-91d86b608df2)
