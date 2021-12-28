# 2021 빅콘테스트 데이터분석분야 챔피언리그 수산Biz
[수산Biz](https://www.bigcontest.or.kr/points/content.php#ct04)<br>
**제공된 데이터는 대회 출품을 위한 목적에 한해 사용가능 하므로 비공개**
## 문제정의
![alt pic1](/pic/pic1.png)

# 목차
* 그래프 폰트 한글 설정
* 라이브러리 임포트
  * 드라이브 마운트

**1. 오징어 가격 예측**
* 데이터프레임
* 데이터프레임에서 오징어만 추출 후 이상치 제거 및 전처리
* 라벨인코딩 작업
* 모델링
* Input 데이터인 20년도 df 정의 및 전처리
* 오징어 가격 예측 정답

**2. 연어 가격 예측**
* 데이터프레임에서 연어만 추출 후 이상치 제거 및 전처리
* 라벨인코딩 작업
* 모델링
* Input 데이터인 20년도 df 정의 및 전처리
* 연어 가격 예측 정답

**3. 흰다리새우 가격 예측**
* 데이터프레임에서 흰다리새우만 추출 후 이상치 제거 및 전처리
* 라벨인코딩 작업
* 모델링
* Input 데이터인 20년도 df 정의 및 전처리
* 흰다리새우 가격 예측 정답

## 그래프 폰트 한글 설정
아래 셀 실행 후 런타임 다시시작
![alt pic2](/pic/pic2.png)
## 라이브러리 임포트
![alt pic3](/pic/pic3.png)
## 드라이브 마운트
![alt pic4](/pic/pic4.png)<br>
data 폴더 생성 후 제공데이터 및 자율평가데이터, squid.h5, salmon.h5, shrimp.h5를 data 폴더에 업로드 후 전체 실행

## 데이터프레임
![alt pic5](/pic/pic5.png)<br>
분석에 사용할 제공 데이터프레임

# 오징어 가격 예측
## 제공df에서 오징어만 추출 후 IQR을 활용하여 이상치 제거 및 전처리
![alt pic6](/pic/pic6.png)<br>
![alt pic7](/pic/pic7.png)<br>

이상치를 제거해도 된다고 판단한 이유는 미래에는 천재지변으로 인한 수산물 가격의 급등 혹은 급락이 없을 것이라고 가정한 후에 예측을 진행할 것이기 때문
* 각년도 별로 데이터가 수집된 일자가 다르기 때문에 월 별로 Week_Number(1년 중 몇 번째 주차인지)를 기준으로 데이터를 정렬해야 함
* 제공된 데이터 중 16년부터 19년의 데이터를 활용할 것이고 또한 2015년인 데이터는 오직 12월 28일의 데이터만 있기 때문에 활용하지 않을 것이므로 제거
* 년도 별로 수집된 데이터의 시작 요일이 다르므로 구분하여서 Week_Number를 산출하였음 ex)16년과 17년의 데이터의 수집시작 요일은 일요일이나 18년과 19년의 데이터의 수집시작 요일은 월요일임

## 16~19년도 별 가격 변동의 추세 확인
* 오징어 가격에는 1년의 추세가 존재한다고 판단<br>
* 16년도<br>
![alt pic8](/pic/pic8.png)
* 17년도<br>
![alt pic9](/pic/pic9.png)
* 18년도<br>
![alt pic10](/pic/pic10.png)
* 19년도<br>
![alt pic11](/pic/pic11.png)

## 년도 별로 나누었던 데이터를 다시 병합 후 YEAR과 Week_Number 기준으로 정렬 및 전처리 한 데이터프레임
![alt pic12](/pic/pic12.png)

## 라벨인코딩 작업
* 활용할 수 있는 feature가 모두 범주형이므로 정수 인코딩
![alt pic13](/pic/pic13.png)

## 중복 제거 및 높은 빈도 수를 가진 단어일수록 낮은 정수 인덱스 부여 및 빈도 수가 1인 단어 제거
![alt pic14](/pic/pic14.png)

## 범주형 값들을 인코딩 값으로 교체한 df
![alt pic15](/pic/pic15.png)<br>
해당 df를 YEAR와 Week_Number로 groupby를 진행 한 뒤 각 주차별로 평균을 산출하여 모델에 활용

## 모델링
모델은 지난 1년 간의 데이터로 1년 후를 예측하는 모델이므로 Target은 1년후의 실제 가격임 따라서 16,17,18년 데이터로 각각 1년 후를 예측하는 모델을 생성 후 해당 모델에 19년도의 데이터를 넣어서 20년의 가격을 예측<br>
![alt pic16](/pic/pic16.png)<br>
![alt pic17](/pic/pic17.png)

## 16,17,18년 데이터로 각각 1년 후를 예측한 결과
![alt pic18](/pic/pic18.png)

## 20년도 df 정의 및 동일한 방식으로 전처리
![alt pic19](/pic/pic19.png)

## 19년도 데이터를 모델에 투입한 결과와 실제 20년도 값을 비교한 결과
![alt pic20](/pic/pic20.png)

## 20년도 데이터를 input하여 21년도 오징어 가격을 산출하여 최종 답안으로 제출
![alt pic21](/pic/pic21.png)

## 2021년 1월부터 6월까지의 오징어 예측 가격(최종 답안)
![alt pic22](/pic/pic22.png)

# 연어, 흰다리새우 가격 예측
* 연어와 흰다리새우 모두 오징어와 같은 방식을 통해 답안을 도출하였음
* 연어에는 계절적인 추세가 있다고 판단하였음(3개월 주기)
* 흰다리새우에는 1달의 추세가 있다고 판단하였음

## 2021년 1월부터 6월까지의 연어 예측 가격(최종 답안)
![alt pic23](/pic/pic23.png)
## 2021년 1월부터 6월까지의 흰다리새우 예측 가격(최종 답안)
![alt pic24](/pic/pic24.png)
