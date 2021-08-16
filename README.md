# Water-Quality-Prediction-Model

## 목적 : 충청권 수질 예측

- **Data**

    ![image](https://user-images.githubusercontent.com/61724682/127329159-32afbb04-e707-4a80-86a7-8b653fb13ea2.png)

  **[물환경 정보 시스템](http://water.nier.go.kr/waterData/generalSearch.do?menuIdx=3_1&siteTypeCd=A#none) 해당 사이트에서 데이터 다운로드**
    - data example 
        - 2011년 1월 부터 2021년 6월까지의 수질 측정 데이터

        |번호|측정소명|년/월|수소이온농도|용존산소|BOD|COD|부유물질|총질소|총인|TOC|수온(℃)|
        |------|---|---|---|---|---|---|---|---|---|---|---|
        |1|가막|2011/01|7.3|14.1|0.7	|2.1|1.4|4.544|	0.012|1.4|-0.5|
        |2|가막|2011/02|7.3|15.5|0.8	|3.3|3.8|4.542|	0.031|1.8|0.3|
        |3|가막|2011/03|7.4|14.2|1.1	|3.5|6.1|3.746|	0.031|1.4|7.8|
        |4|가막|2011/04|7.8|11.1|1.3	|3.5|5.6|3.228|	0.027|1.8|11.5|
        |5|가막|2011/05|7.8|11|1.1|3.9|8	|3.37|0.043|2.6|16.8|

  **측정소 위치 데이터**
    - data example

        |이름|	주소|	지역	|위도|	경도|
        |------|---|---|---|---|
        |가막	|전라북도 진안군 진안읍 가막리|	금강물환경연구소|	35.816335|	127.51127|
        |갑천1	|대전광역시 서구 정림동|	대전광역시|	36.298785|	127.361663|
        |갑천2	|대전광역시 서구 월평동|	대전광역시|	36.362868|	127.361964|

  **쓰레기 매립지 위치 데이터**
    - data example
  
        |매립장|위도|경도|
        |------|---|---|
        |공주시위생매립장쓰레기매립,소각장|	36.425995	|127.061900|
        |금산군위생매립장쓰레기매립,소각장|	36.170733	|127.444076|


- **지도 시각화**

<img src = "https://user-images.githubusercontent.com/61724682/127346219-cb97d959-a360-4100-8edd-6ae12d3b083f.png" width="30%" height="30%">

   - python 지리 데이터 시각화 라이브러리인 folium 활용

   - BOD값과 COD값을 바탕으로 급수를 나눈 후 시각화

   <img src = "https://user-images.githubusercontent.com/61724682/129497996-379162d9-d7fb-4377-acab-cb7ca7fb9d7f.png" width="60%" height="60%">

   - 결과
   - 1급수~6급수 'blue', 'cadetblue', 'lightgreen', 'yellow , 'orange', 'red' 
   
<img src = "https://user-images.githubusercontent.com/61724682/129497864-ef283aba-614b-4f95-bbab-bceb68b5a622.PNG" width ="500" />   <img src = "https://user-images.githubusercontent.com/61724682/129498167-ba99aab1-273a-43f0-9e11-32ad23e9e051.PNG" width ="460" />

   - 해석
       - 작성하기
### 모델링
   - 7년 간 관측된 수질 측정값으로 arima 모델을 학습을 시킨 후 3년 기간의 데이터로 검증을 하고 마지막 달인 5월의 데이터로 예측값 생성

   - 성능지표 
        - rmse :모델이 예측한 값과 실제 환경에서 관찰되는 값의 차이를 다룰 때 흔히 사용하는 측도
        - rmse값이 작을수록 예측력이 좋은 것 => 실제 환경과 관찰되는 값의 차이가 작은 것

- **ARIMA model**

<img src = "https://user-images.githubusercontent.com/61724682/129498336-4afc3ba7-936d-49c9-99e0-4770093d8f4c.png" width ="400" />   <img src = "https://user-images.githubusercontent.com/61724682/129498357-23e433f8-670d-4992-8e84-f321c0cf2b21.png" width ="400" />

   - 갑천4 / BOD(㎎/L) 성능(rmse값) : 0.7780475078967
   - 예측값 : 2.732392610697287


<img src = "https://user-images.githubusercontent.com/61724682/129498497-118b9741-c043-49d5-bb28-3b2e494459de.png" width ="400" />   <img src = "https://user-images.githubusercontent.com/61724682/129498509-06242734-3152-4c40-8129-1d0021018fc9.png" width ="400" />

   - 미호천5 / COD(㎎/L) 성능(rmse값) : 2.342095190878987
   - 예측값 : 8.919815910530707


<img src = "https://user-images.githubusercontent.com/61724682/129498547-48f67cc7-9c5c-48a9-845e-6941b9bcf66b.png" width ="400" />   <img src = "https://user-images.githubusercontent.com/61724682/129498554-965b9d11-7d48-447d-a511-a22cd8559c28.png" width ="400" />

   - 간월호1 / 용존산소(㎎/L) 성능(rmse값) : 3.6131033950193436
   - 예측값 : 11.21310914934322

- **LSTM model**

