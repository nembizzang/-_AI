# 1. data 다운로드 : 
https://drive.google.com/drive/folders/1rOQX10SQSjqZCMlkP__F3yir2N74fIWd?usp=sharing

<br>

# 2. data directory 구성
```
├── dataset
│   ├── tot_images     # whole raw data
│   ├── whole_stage_test     # stage1~3를 모두 확인하는 test            
│   ├── train     # stage 1 not augmentated data(train)
│   ├── valid     # stage 1 not augmentated data(train)
|   │   ├── images
|   │   ├── labels
|   │   ├── labels_hbb     # labels for horizontal bounding box (cx,cy,w,h)
|   │   ├── labelTxt_obb     # labels for oriented bounding box(x1,y1,x2,y2,x3,y3,x4,y4,category,difficulty)
|   │   └── labelTxt_raw     # labelImg OBB labeling raw (category,cx,cy,w,h,theta)
│   ├── train_grayscale     # stage1 only grayscale data(train)
│   ├── valid_grayscale     # stage1 only grayscale data(valid)
|   │   ├── images
|   │   └── labels
│   ├── title_raw     # stage2 whole title data
│   ├── train_title     # stage2 whole title data(train)
│   ├── valid_title     # stage2 whole title data(valid)
│   ├── test_title     # stage2 whole title data(test)
|   │   ├── images
|   │   └── labels
│   ├── train_title_color     # stage2 only color title data(train)
│   ├── valid_title_color     # stage2 only color title data(valid)
|   │   ├── images
|   │   └── labels
|   ├── data.yaml     # stage1 whole data(augmentation data) train/valid에 활용
│   ├── data_grayscale.yaml     # stage1 only grayscale data train/valid에 활용
│   ├── data_title.yaml     # stage2 whole data(augmentation data) train/valid에 활용
│   └── data_title_color.yaml     # stage2 only color data train/valid에 활용
```

<br>

# 3. final model data 개수

|Stage1 - 책 영역 검출|Stage2 - 제목 영역 검출|Whole Stage - 사용자 Input ~ Title|
|:---:|:----:|:----:|
|Train : 3510개 (80%)|Train : 4896개(80%)|-|
|Valid : 900개 (20%)|Valid : 1242개 (20%)|-|
|-|-|Test : 책장 image 13개(제목 310개)|
|Total : 4410개|Total : 6138개|Total : 13개(제목 310개)|