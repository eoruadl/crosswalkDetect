# 3차 미니프로젝트
## 주제: 자동차 주행 중 객체인식을 통한 우회전 판단 모델 구현
- 목적: 딥러닝 기술을 학습하기 위해 객체인식 모델을 사용해본다.
- 기술 스택: 파이썬, 파이토치, YOLOV5, OpenCV 라이브러리,Roboflow

![image](https://user-images.githubusercontent.com/108312160/196027904-be9fbf4b-4f35-4313-9769-edfc8bfb93ac.png)


## 기획의도: 보행자 안전규정을 강화한 새로운 개정 교통법이 시행되면서 교차로 우회전 시 고려해야할 부분이 생겨 개정법에 익숙하지 않은 운전자에게 신호를 주어 교통법 위반을 방지하기 위한 모델을 구현하는 것이 목적

## 참조 : 레포지토리 내의 ppt파일 참조

### 데이터 준비

- 학습을 위한 테스트데이터 준비

- 횡단보도, 보행자신호등, 보행자 데이터를 병합

![image](https://user-images.githubusercontent.com/108312160/196027225-387cd8c4-5188-4d64-bc17-0545965c04e9.png)
- 실제 촬영환경의 변화(조도, 각도, 날씨 등)에 인식정도를 개선하기 위해 augmentation 부여

![image](https://user-images.githubusercontent.com/108312160/196027358-9026b901-acff-4af2-b60b-5ef25b861a97.png)

### 학습모델
- Pytorch 라이브러리의 Yolov5 모델 사용

![image](https://user-images.githubusercontent.com/108312160/196027430-8cd41ae8-084c-4116-9c1b-cb0cc68eff2c.png)

- Yolo내 가중치별 학습모델 학습성과

![image](https://user-images.githubusercontent.com/108312160/196027455-06f52296-507f-46b3-9622-8c54e8d59f4e.png)

### 학습결과
- 학습된모델(.onnx)을 통해 입력된 영상에서 프레임단위로 이미지추출, 학습된 객체를 판별
- 인식된 객체 리스트를 설정 신뢰도 기준에 따라 필터링
- 필터링된 객체 리스트에서 class_id, x, y, width, height 정보 추출
- 출력된 값을 기준으로 이미지층에 boundbox 작성

![image](https://user-images.githubusercontent.com/108312160/196027533-308bf14b-72e9-4363-9988-4c2b8fb2fbf9.png)
