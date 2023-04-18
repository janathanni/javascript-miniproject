# 자바스크립트를 통한 사진 처리 기능  
# 프로젝트 소개
> 이 프로젝트는 자바스크립트의 canvas를 이용하여, 사진을 처리하는 여러 가지 기법을 다룹니다. 다양한 화소점 처리, 기하학 처리, 화소영역 처리, 그리고 히스토그램 처리 기법을 구현하여 이미지를 다양하게 가공할 수 있습니다.  

# deploy 주소
## https://janathanni.github.io/javascript-miniproject/

# 기능  <br>
##  화소점 처리
> 화소점 처리는 다른 화소의 영향 없이, 화소점의 값만 변경하는 것을 의미합니다.  

### 1. 밝기 조절
이미지의 밝기를 조절합니다.
![밝아짐](/src/brightness2.png)
![어두워짐](/src/brightness1.png)
### 2. 반전
이미지를 반전시킵니다.
![어두워짐](/src/inversion.png)
### 3. 흑백 처리
이미지를 흑백으로 변환합니다. 평균값과 중위수 두 가지 방법으로 구현합니다.

## 기하학 처리
> 기하학 처리는 영상 내에 있는 화소들의 배치를 변경하는 것을 의미합니다. 영상의 회전, 확대 및 축소가 이에 해당합니다.

### 1. 축소
이미지를 축소합니다.
### 2. 확대
이미지를 확대합니다. 일반적인 방법과 백워딩 방법 두 가지로 구현합니다.
### 3. 회전
이미지를 회전합니다. 일반적인 방법과 백워딩 방법 두 가지로 구현합니다.

## 화소영역 처리
> 화소영역 처리는 화소의 값만을 변경하는 처리가 아니라, 그 주위의 화소값도 함께 고려하는 것을 의미합니다.

### 1. 엠보싱
이미지에 엠보싱 효과를 적용합니다.
### 2. 블러링
이미지를 블러처리합니다.
### 3. 윤곽선 추출
이미지의 윤곽선을 추출합니다.

## 히스토그램 처리
> 히스토그램 처리는 히스토그램 정보를 이용하여, 화소값들의 분포도를 조정하는 것을 의미합니다.
### 1. 히스토그램 스트래칭
이미지의 히스토그램을 스트래칭하여 대비를 개선합니다.
### 2. 엔드-인 탐색
이미지의 엔드-인 값을 조정하여 대비를 개선합니다.
### 3. 평활화
이미지의 히스토그램을 평활화하여 대비를 개선합니다.