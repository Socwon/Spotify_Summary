## MobileBERT를 활용한 노래 가사 요약 프로젝트  
<!-- 
badge icon 참고 사이트
https://github.com/danmadeira/simple-icon-badges
-->
<img src="https://img.shields.io/badge/python-%233776AB.svg?&style=for-the-badge&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/pytorch-%23EE4C2C.svg?&style=for-the-badge&logo=pytorch&logoColor=white" /> <img src="https://img.shields.io/badge/pycharm-%23000000.svg?&style=for-the-badge&logo=pycharm&logoColor=white" />

## 1. 개 요 A4용지로 1장정도 (그림포함)
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

데이터는 57494건이 있다.

### 2.2 추출한 데이터
노래를 가장 많이 낸 아티스트와 노래를 가장 적게 낸 아티스트

<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/baa3f96f-1514-4227-8e51-9ef679c2ce3a"/>
<br>
<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/107210c5-f925-498e-a112-25f3f276ecd2"/>
노래를 가장 많이 낸 아티스트 15명과 노래를 가장 적게 낸 아티스트 15명을 그래프로 시각화하여 출력한 결과, 제일 노래를 많이 낸 아티스트는 Donna Summer이며 노래는 191개이고 제일 노래를 적게 낸 아티스트는 5명이며 노래는 1개씩 냈다.
 

### 2.3 추출한 데이터에 대한 탐색적 데이터 분석
1~5점 척도인 경우에는 분포
리뷰 문장의 길이
연도별, 장소별 등등 데이터의 부가정보를 바탕으로 데이터를 탐색 (pandas, matplotlib)

# 여기까지가 중간 과제 점검 

## 3. 학습 데이터 구축

## 4. MobileBERT 학습 결과

## 5. 느낀점 및 배운점
