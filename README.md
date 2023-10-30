# 객체 인식을 통한 무인 점포 시스템

졸업 프로젝트로 '무인 점포를 위한 영상내 객체 인식 및 추적용 알고리즘 개발'을 주제로 연구를 하였습니다.



## Auto-labeling

기존 객체 인식 알고리즘 개발에서 주로 사용되는 train set은 manual-labeling으로 만들어진 사진들입니다. 사람이 직접 사진을 찍고 물품을 라벨링하는 manual-labeling은 많은 시간과 비용이 소모됩니다. 이러한 문제를 해결하기 위해 auto-labeling을 도입하였습니다. Cut and paste 방식으로 여러 배경 사진과 다양한 물품들을 자동으로 합성하여 라벨링할 수 있도록 프로그래밍 해 train set의 양을 늘렸습니다.

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/0d72f88e-44dd-4d9d-8866-9fc065e23413)

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/977c8d44-75c7-4218-bbf6-5802aed3e55e)

manual-labeling (좌측), auto-labeling (우측)



## Data augmentation

객체 인식 모델을 학습시킬 때 최대한 다양한 환경에서 물건을 찍은 것처럼 데이터의 양을 늘리고자 data augmentation을 수행하였습니다. Python으로 color change, gamma change, size change, hsv change, rotation의 총 다섯가지 data augmentation 기법을 사용하는 코드를 작성하였습니다.

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/3a1a9040-137d-4c0a-ba19-d59008339fe0)

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/ad05373b-cf9d-494c-9b0c-d2795c3f9c68)

원본(좌측), rotate 수행(우측)



## GP-GAN with content loss

기존의 cut and paste 방식으로 물품들을 합성할 경우 물건을 cut 하는 과정에서 foreground 물체의 윤곽선에 생긴 검은색 테두리가 존재했습니다. 이 테두리가 물체의 일부인 것처럼 학습할 경우 인식률이 낮아지기 때문에 이 테두리를 없애고자 GP-GAN을 사용하였습니다. GP-GAN을 그대로 사용할 경우 foreground와 background의 간격을 줄이고자 물품인 foreground가 지나치게 손상되는 경우가 발생하였습니다. 이를 해결하기 위해 GP-GAN에 content loss 방식을 도입하였습니다. 결과적으로 인식률 개선에는 크게 도움이 되지 못했습니다.

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/327021a5-46ba-4c82-8171-1015dfc44f77)

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/bb1a7403-a052-48ef-9eaa-f0f8b9b8859a)



## Weight Sensor

객체 인식만으로는 물품 출입 인식에 한계가 있었습니다. 뒤에 가려진 물품이 사라질 경우, 새로운 물품이 기존 물품을 가릴 경우 등 카메라만으로는 정확히 인식하기 어려운 상황이 있습니다. 이를 보완하기 위해 아두이노에 무게 센서를 연결하고 판매대 아래에 부착해 실시간으로 판매대의 무게를 측정하였습니다. 아두이노에 각 물품의 무게를 저장시켜 놓고 무게가 변화했을 때 각 물품들에 대한 고유한 무게 데이터를 기반으로 어떤 물품이 출입하였는지 출력하도록 시스템을 개발했습니다.

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/f088cef6-95fc-44d7-ad5f-d9e0bf2322c3)



## Multi Camera

카메라 한 대 만으로는 앞면이 비슷한 물체, 뒤에 가려진 물체 등을 볼 수 없다는 문제를 해결하기 위해 여러 각도에 카메라를 설치하여 이를 보완하였습니다. 좌측, 정면, 우측에 한 대씩 카메라를 설치하여 동시에 인식하도록 하였습니다.

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/7c5d3797-99ed-4d8d-92f2-fbb68cdb30b6)

![image](https://github.com/jiwoo219/unmanned-store/assets/78020027/83cd37c6-1561-40eb-9150-7bc424fcdf66)
