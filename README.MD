<img src="https://github.com/Socwon/Spotify_Summary/assets/101037584/13b559d7-7593-4f7b-832e-623fb1ee88b1" width="700" height="200"/>

## T5를 활용한 노래 제목 예측 프로젝트  
<div>
<img src="https://img.shields.io/badge/python-%233776AB.svg?&style=for-the-badge&logo=python&logoColor=white"/> 
<img src="https://img.shields.io/badge/pytorch-%23EE4C2C.svg?&style=for-the-badge&logo=pytorch&logoColor=white"/> 
<img src="https://img.shields.io/badge/pycharm-%23000000.svg?&style=for-the-badge&logo=pycharm&logoColor=white"/>
</div>

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
| Aerosmith | The Hand That Feeds | /z/zz+top/36+22+36_20149356.html  | Doctor, doctor, doctor Please, doctor, doctor, please Doctor, doctor, doctor Feel like a ol...  |
| .. | .. | ...  | ...  |
| ZZ Top | 36-22-36 | /b/barbra+streisand/i+wont+last+a+day+without+you_20699679.html  | What, what, what you want? Hey My thing is a real fine thing It's a thing, it's a real fine th...  |
| ZZ Top | 2000 Blues | /z/zz+top/2000+blues_10198797.html  | A hundred thousand dollars Wouldn't touch the price I paid Of the hundred thousand moments ...  |

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


## 3. 학습 데이터 구축
#### 패키지
<div>
<img src="https://img.shields.io/badge/transformers-409FFF?style=flat-square&logo=transformers&logoColor=white"/>
<img src="https://img.shields.io/badge/torch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white"/>
<img src="https://img.shields.io/badge/numpy-013243?style=flat-square&logo=numpy&logoColor=white"/>
<img src="https://img.shields.io/badge/scikit-learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white"/>
</div>
<br>

### 3.1 학습 데이터와 분석 데이터
| artist | summary | text  | 
|-------|-----|-------|
|Unwritten Law|Genocide| Well who are you what do you know And I guess it only goes to show Don't think you're ready for the fall Do you think you really wanta play.. |
| Tori Amos | Butterfly | Stinky soul get a little lost in my own Hey General, need a little love in that hole of yours One ways, now, and..|
| Glee | Dark Side | There's a place that I know It's not pretty there and few have ever gone If I show it to you now Will it make you run away.. |
| John Denver | Downhill Stuff | Blue river blues I'd rather be outside Here I am inside Watching it rain Blue river blues I'd rather be somewhere.. | 
| Judy Garland | Why Was I Born? | Why was I born? Why am I livin'? What do I get? What am I givin'? Why do I want a thing I.. | 

원본 데이터셋의 link열은 삭제하였으며 song열의 이름을 summary로 변경하고 모델 학습의 효율성을 높이기 위해 3000개의 샘플을 랜덤으로 추출하여 만들었다.
그 후 원본 데이터셋을 위와 같은 조건으로 5000개의 데이터를 랜덤으로 추출하여 학습된 요약 모델을 적용시켰다.



## 4. T5 학습 결과



### 4.1 결과


### 4.2 모델 평가


## 5. 느낀점 및 배운점
