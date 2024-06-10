<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/13b559d7-7593-4f7b-832e-623fb1ee88b1" width="700" height="200"/>

## BERT를 활용한 노래 제목 예측 프로젝트  
<!-- 
badge icon 참고 사이트
https://github.com/danmadeira/simple-icon-badges
-->
<img src="https://img.shields.io/badge/python-%233776AB.svg?&style=for-the-badge&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/pytorch-%23EE4C2C.svg?&style=for-the-badge&logo=pytorch&logoColor=white" /> <img src="https://img.shields.io/badge/pycharm-%23000000.svg?&style=for-the-badge&logo=pycharm&logoColor=white" />

## 1. 개 요 
### 1.1 노래 제목의 영향력
노래 제목은 노래의 핵심을 나타내며, 듣는 이들에게 노래의 주제나 감정을 전달하는 역할을 한다. 노래 제목은 노래를 소개하고, 청취자의 관심을 끌고, 노래의 주제나 감정을 전달하는 역할을 한다. 대중적인 장르의 경우 노래의 의미가 명확해지는 것이 중요하며, 노래 제목은 노래 전체에서 가장 기억에 남는 부분이어야 하므로 명확성이 중요하다. 이는 노래의 인기와 성공에 영향을 미치는 요소 중 하나이며 또한 마케팅적으로도 중요하고, 청취자의 호기심을 자극하여 노래를 들을 가능성을 높일 수 있다. 따라서 노래 제목을 의도적으로 선택하는 것이 중요하다.

(출처 : https://soundfly.com/courses/intro-to-scoring-for-film-and-tv?utm_source=Flypaper&utm_campaign=Flypaper-ad-system&utm_medium=sidebar-ad)

### 1.2 문제 정의
Spotify Million Song Dataset는 스포티파이라는 음악 앱의 노래 이름, 아티스트 이름, 노래 링크 및 가사가 포함 되어 있는 데이터셋이다. 노래 추천, 노래 분류 등에 사용할 수 있으며 이 프로젝트에서는 대부분의 사람들이 즐겨 듣는 노래는 어떤 내용의 가사가 담겨져 있으며 이에 따른 제목이 무엇인지 예측하는 인공지능 모델을 개발하고자 한다.

## 2. 데이터
### 2.1 원시 데이터
[Spotify Million Song 데이터셋](https://www.kaggle.com/datasets/notshrirang/spotify-million-song-dataset)<br/>
[Spotify 홈페이지](https://open.spotify.com/)

- 데이터명

| artist | song | link  | text  |
|-------|-----|-------|-------|
|아티스트 이름|노래 제목| 노래 링크 | 노래 가사 |

- 활용할 데이터 예시

| artist | song | link  | text  |
|-------|-----|-------|-------|
|Alison Krauss|Maybe| /a/alison+krauss/maybe_20006156.html | Yesterday the odds were stacked In favor of my expectations Flyin' above the rest, Never fa... |
| Aerosmith | The Hand That Feeds | /a/aerosmith/the+hand+that+feeds_20004218.html  | Doctor, doctor, doctor Please, doctor, doctor, please Doctor, doctor, doctor Feel like a ol...  |
| Arlo Guthrie | The Streets Of Laredo | /a/arlo+guthrie/streets+of+laredo_20328407.html  | As I walked out in the streets of Laredo As I walked out in Laredo one day I spied a poor cowb...  |
| Barbra Streisand | I Won't Last A Day Without You | /b/barbra+streisand/i+wont+last+a+day+without+you_20699679.html  | Day after day I must face a world of strangers Where I don't belong, I'm not that strong It's ...  |

데이터는 총 57494건이 있다.


### 2.2 탐색적 데이터
- 노래를 가장 많이 낸 아티스트 15명과 노래를 가장 적게 낸 아티스트 15명
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/d45fb3e6-8d97-429c-b428-2c11cf36686d" width="700" height="400"/>

제일 노래를 많이 낸 아티스트는 'Donna Summer'이며 노래는 191개이고 제일 노래를 적게 낸 아티스트는 5명이며 노래는 1개씩 냈다.

- 불용어를 제외한 모든 노래 가사에서 자주 등장하는 키워드 5가지
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/98205e6b-d976-4dbd-9d43-9db8ab37a7ed" width="450" height="400"/>

제일 많이 등장한 키워드는 순서대로 "Love", "Time", "One", "Heart", "I'm" 이다.
따라서 사랑, 시간에 관련된 주제의 노래가 많이 발표된다는 것을 알 수 있다.

### 2.3 추출한 데이터에 대한 탐색적 데이터 분석
- 모든 노래의 평균 가사 길이
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/318475fc-1f52-4102-ba87-03f0a6cfdce3"/>

- 모든 노래의 가사 길이 시각화
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/a0cc12b0-4f2f-48e3-aad2-36b7a8677f26" width="700" height="400"/>

평균적으로 100글자에서 300글자 사이의 가사를 가진 노래가 가장 많이 나온다는 것은 음악을 구성하는 가사의 적절한 길이가 중요하다는 것을 보여준다. 따라서 노래 제작자들은 이러한 범위에 가사를 맞추는 것이 노래의 인기와 성공에 도움이 될 수 있다는 것을 고려하며 노래를 제작한다는 것을 알 수 있다.


## 3. 학습 데이터 
학습 데이터를 모두 읽어들인 후 랜덤하게 3000개의 샘플을 추출하여 만들었다. 가사를 기반으로 노래를 분석하고, 입력된 가사와 유사한 노래를 찾은 후에는 해당 노래의 제목을 사용자에게 제공한다.

<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/456956d5-e46b-4f8c-b3d1-609d1b9bb4d4"/>

### 3.1 학습 설정
- 모델: BERT (Bidirectional Encoder Representations from Transformers)
- 미세 조정: 특정 가사에 대응하는 노래 제목을 예측하기 위해 BERT 모델을 미세 조정했다.
- 하이퍼파라미터:
  - 학습률: 2e-5
  - 배치 크기: 8
  - 학습 에포크: 3
  - 가중치 감소: 0.01
- 기타 설정: 로그 기록, 평가 전략은 epoch 단위 등의 설정을 적용했다.

## 4. BERT 학습 결과
#### 개발환경  

<img src="https://img.shields.io/badge/python-%233776AB.svg?&style=for-the-badge&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/pytorch-%23EE4C2C.svg?&style=for-the-badge&logo=pytorch&logoColor=white" /> <img src="https://img.shields.io/badge/pycharm-%23000000.svg?&style=for-the-badge&logo=pycharm&logoColor=white" />

BERT 모델을 활용하여 가사 기반의 노래 제목 예측 학습을 진행했다. 미리 훈련된 BERT 모델을 사용했으며, 학습 데이터는 전처리된 가사와 해당 가사에 대응하는 노래 제목을 매핑한 데이터로 구성되었다. Google의 BERT 모델을 기반으로 학습을 진행하며, GPU 가속을 활용하여 학습 성능을 향상시켰다.

### 4.1 결과
학습된 BERT 모델은 학습 데이터에서 노래 제목 예측을 수행하였으며, 다음과 같은 결과를 얻었다.
- 학습 손실: 평균 손실은 0.3으로, 학습 과정에서 모델의 성능을 모니터링
- 검증 정확도: 학습된 모델은 검증 데이터에서 약 85%의 정확도

### 4.2 모델 평가
테스트 데이터에서 모델을 평가하였으며, 다음과 같은 결과를 얻었다.
- 테스트 정확도: BERT 모델은 테스트 데이터에서 약 82%의 정확도
- 추론 속도: 모델은 입력 가사에 대해 빠르게 예측을 수행하였으며, 추론 시간은 평균 0.1초 이내

## 5. 느낀점 및 배운점
