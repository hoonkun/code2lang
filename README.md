# Project: Code2Lang
사용 IDE: Intellij IDEA Ultimate  
작성자: 김영웅 (Github: gohoon-k)  
작성일: 2021년 02월 18일 11시 24분

## 따라해보기
아래 프로그램/라이브러리를 모두 설치하고 필요한 명령을 실행하여 프로젝트를 다시 실행해볼 수 있습니다.

### 필요사항
- ```node 14.15.4``` 가 설치되어있을 것(웹 프로젝트를 실행할 경우에만)
- ```python 3.8.7```이 설치되어있을 것
- python module 은 conda 가상환경을 이용하지 않으므로 system interpreter 에 설치해야한다(pip install).
    - ```tensorflow 2.4.0``` 가 설치되어있을 것
    - ```keras 2.4.3``` 가 설치되어있을 것
    - ```numpy 1.18.5```가 설치되어있을 것(최신버전(1.19)의 경우 윈도우 운영체제에서 에러가 나므로 반드시 1.18.5를 설치할 것)
    - ```bs4``` 가 설치되어있을 것(웹 스크래핑 코드를 실행할 경우에만)
    
### 새로운 모델을 만들어 학습시키기
새로운 모델을 만들어 학습을 수행하려면 ```sources.machine_learning.train``` 스크립트를 실행합니다.  
실행하면 ```models``` 디렉토리에 스크립트를 실행한 시점의 시간이 이름으로 된 디렉터리가 새로 생성될 것입니다.  
이 디렉토리에 새롭게 생성된 모델이 저장됩니다.

### 모델의 학습 상황을 텐서보드를 사용해 확인하기
텐서보드를 사용해 모델의 훈련 정보를 확인하려면 명령창에서 이 프로젝트의 위치로 이동한 후 다음 명령을 실행하고 브라우저에서 ```localhost:6006```으로 이동합니다.
```
code2lang>tensorboard --logdir train_logs
```

### 예측을 수행할 때 만든 모델을 사용하도록 설정 변경하기
새롭게 학습시킨 모델을 웹 프로젝트에서 예측을 수행할 때 사용하는 모델로 설정하려면 ```sources.constants``` 스크립트의 ```PREDICT_MODEL``` 상수의 값을
학습이 완료된 모델이 저장된 경로(날짜와 시간)로 설정합니다.

### 웹 프로젝트를 통해 실제 예측을 수행해보기
웹 프로젝트를 실행하려면 명령창에서 현재 이 프로젝트의 위치로 이동한 후 다음 명령을 실행하고 브라우저에서 ```localhost:8080```로 이동합니다.  
__주의__: 반드시 프로젝트의 루트 디렉터리에서 진행해야합니다. ```web_output_react/backend``` 디렉터리로 이동하여 실행하면 모듈을 찾을 수 없다는 메시지가 출력될것입니다.
```
code2lang>node web_output_react/backend/entry.js
```

## 디렉토리 구조
- datasets: 최종적으로 모델의 학습에 사용할 데이터들이 저장된 디렉터리.
  - train_dataset: 훈련에 사용된 데이터집합
  - validation_dataset: 검증에 사용된 데이터 집합
- models: 학습 과정을 통해 정해진 weight 과 bias 등의 값을 모두 저장해서, 로드했을 때 학습 직후의 상태를 복원할 수 있는 파일들이 저장된 디렉터리.
- scraping: 스크래핑 작업이 진행되는 곳으로 통계 파일, 스크랩한 파일 등이 있는 디렉터리.
- sources: 파이썬 소스코드가 저장된 디렉터리.
  - data_analyzing: 데이터 분석을 수행하는 스크립트가 포함된 패키지
  - data_processing: 데이터 분석에 사용되는 클래스가 포함된 패키지
  - data_scraping: 웹 스크래핑을 수행하는 스크립트가 포함된 패키지
  - data_visualization: 데이터 시각화 과정을 수행하는 스크립트가 포함된 패키지
  - dataset_creation: 스크래핑 작업 디렉토리로부터 실제 데이터 집합을 만들어내는 스크립트가 포함된 패키지
  - machine_learning: 모델의 학습, 예측 등을 수행하는 스크립트가 포함된 패키지
- train_logs: 모델의 훈련 때 기록된 텐서보드 로그가 저장되는 디렉터리.
- visualized_data: 학습할 데이터들만 가지고 통계를 내려 그래프로 그린 결과 파일들이 저장된 디렉터리.
- web_output_react: 학습된 모델을 가지고 실제 예측을 할 때 사용되는 웹 페이지 프로젝트. React 로 제작되어있다.
  - backend: node js 스크립트가 포함된 디렉터리.
  - build: react 스크립트가 컴파일되어 저장된 디렉터리
  - public: 웹에서 public하게 사용할 리소스가 저장된 디렉터리
  - src: react 스크립트가 포함된 디렉터리
