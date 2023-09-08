# ****Book is On&On - 책장 이미지를 활용한 디지털 서재 서비스****
## KT AIVLE School 3기 AI track 김영빈

<br>

## Goal & Role
- 주제 : Book is On&On - 책장 이미지를 활용한 디지털 서재 서비스
- 역할 :  AI 모델 알고리즘 개발

<br>

## 모델 알고리즘
|stage|내용|사용 모델|비고|
|:-:|:-:|:-:|:-:|
|Stage 1|책장 이미지로부터 개별 책 영역 검출|yolov8 segmentation|8n 가중치 사용(pretrained by COCO dataset)|
|Stage 2|개별 책 영역으로부터 제목 영역 검출|yolov8 segmentation|8n 가중치 사용(pretrained by COCO dataset)| 
|Stage 3|제목 영역으로부터 제목 문자 인식|Google vision OCR|API 활용|

<br>

## 개발 환경
> Colab Pro  
Python: 3.10.12  
GPU: A100, V100 or T4
RAM: 24.45GB  
Pytorch: 2.0.1+cu118  
cuda version: 11.8
> 

<br>

## Directory
```
├── application.py
├── img2flask.ipynb
├── img2title.ipynb
├── Image Augmentation.ipynb
├── Image Augmentation_grayscale.ipynb
├── requirements.txt
├── Data.md     # 용량 관계로 data는 이 file 내 링크 참조
├── stage1_best.pt
└── stage2_best.pt
```

<br>

## File Description
1) application.py
    - WAS 서버로부터 image를 request 받아 text를 response 해주는 flask 서버
    - WAS 서버와 ngrok으로 연동
2) img2flask.ipynb
    - application.py를 단계별로 실행하는 노트북 파일
3) img2title.ipynb : 2 stage로 구성된 노트북 파일
    - Preprocessing : YOLOv5_OBB label data를 YOLOv8의 segmentation label data로 변경
    - Segmentation : Stage 1 모델을 train 및 predict
    - Crop One book : Stage 1 모델에서 검출된 개별 책 영역을 crop
    - Text Extract : Google vision OCR API 활용 책 제목 인식
4) Image Augmentation.ipynb : image 및 label 회전 증강
5) Image Augmentation_grayscale.ipynb : image 및 label grayscale 증강
6) requirements.txt : 필요 라이브러리 설치
7) Data.md : stage 별 학습 데이터 다운로드 링크 및 경로 설명
8) stage1_best.pt : stage 1 모델 가중치
9) stage2_best.pt : stage 2 모델 가중치
10) 책장 이미지를 활용한 디지털 서재 서비스.pdf : 최종 발표 자료

<br>

## Performance
1. 결과 이미지
- Stage 1 : 개별 책 영역 검출
  ![](https://velog.velcdn.com/images/nembizzang/post/da3362d3-dfc0-432a-9d65-6c8edb22ae1c/image.png)

- Stage 2 : 제목 영역 검출
  ![](https://velog.velcdn.com/images/nembizzang/post/6e35f90f-a55f-4103-9e2b-cb5afb9ac377/image.png)

- Stage 3 : 제목 문자 인식
  ![](https://velog.velcdn.com/images/nembizzang/post/29b53185-3544-44ca-a011-2b9cb2758a14/image.png)

2. 성능
  - 전체 서비스 성능(1~3 stage) : 74.3%
  - stage1, stage2 model 성능
  ![](https://velog.velcdn.com/images/nembizzang/post/ff8d5ccb-f304-4c1f-abc5-675c78f4b860/image.png)