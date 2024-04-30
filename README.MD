<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/13b559d7-7593-4f7b-832e-623fb1ee88b1"/>

## MobileBERT를 활용한 노래 가사 요약 프로젝트  
<!-- 
badge icon 참고 사이트
https://github.com/danmadeira/simple-icon-badges
-->
<img src="https://img.shields.io/badge/python-%233776AB.svg?&style=for-the-badge&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/pytorch-%23EE4C2C.svg?&style=for-the-badge&logo=pytorch&logoColor=white" /> <img src="https://img.shields.io/badge/pycharm-%23000000.svg?&style=for-the-badge&logo=pycharm&logoColor=white" />

## 1. 개 요 
### 1.1 문제 정의
Spotify Million Song Dataset는 스포티파이라는 음악 앱의 노래 이름, 아티스트 이름, 노래 링크 및 가사가 포함 되어 있는 데이터셋이다. 노래 추천, 노래 분류 등에 사용할 수 있으며 이 프로젝트에서는 대부분의 사람들이 즐겨 듣는 노래는 어떤 내용의 가사가 담겨져 있는지 요약된 가사를 생성하는 인공지능 모델을 개발하고자 한다.

### 1.2 노래 가사의 영향력
노래의 가사는 특정 감정을 전달하거나 공감을 일으키는 데 도움을 줄 수 있으며 창의성과 예술적 가치를 통해 청취자들에게 영감을 주고 인상을 남길 수 있다. 이러한 노래들은 종종 문화적으로 영원한 영향력을 행사하며 다수의 사람들에게 기억된다. 따라서 가사는 음악 제작 과정에서 중요한 부분을 차지하며, 노래의 인기와 영향력을 크게 좌우할 수 있다.

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

아티스트 데이터는 643건, 노래 데이터는 44824건, 가사 데이터는 57494건이 있다.


### 2.2 추출한 데이터
- 노래를 가장 많이 낸 아티스트와 노래를 가장 적게 낸 아티스트

<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/baa3f96f-1514-4227-8e51-9ef679c2ce3a"/>

제일 노래를 많이 낸 아티스트는 'Donna Summer'이며 노래는 191개이고 제일 노래를 적게 낸 아티스트는 5명이며 노래는 1개씩 냈다.

- 불용어를 제외한 모든 노래 가사에서 자주 등장하는 키워드 5가지

<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/9b8f5cbe-4de5-487b-8377-21618e0fa9df"/>

제일 많이 등장한 키워드는 순서대로 "Love", "Time", "One", "Heart", "I'm" 이다.
따라서 사랑, 시간에 관련된 주제의 노래가 많이 발표된다는 것을 알 수 있다.

### 2.3 추출한 데이터에 대한 탐색적 데이터 분석
- 모든 노래의 평균 가사 길이
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/318475fc-1f52-4102-ba87-03f0a6cfdce3"/>

- 모든 노래의 가사 길이 시각화
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/a0cc12b0-4f2f-48e3-aad2-36b7a8677f26"/>

평균적으로 100글자에서 300글자 사이의 가사를 가진 노래가 가장 많이 나온다는 것은 음악을 구성하는 가사의 적절한 길이가 중요하다는 것을 보여준다. 따라서 노래 제작자들은 이러한 범위에 가사를 맞추는 것이 노래의 인기와 성공에 도움이 될 수 있다는 것을 고려하며 노래를 제작한다는 것을 알 수 있다.




# 여기까지가 중간 과제 점검 

## 3. 학습 데이터 구축

## 4. MobileBERT 학습 결과

## 5. 느낀점 및 배운점
