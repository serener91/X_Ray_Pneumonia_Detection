# X_Ray_Image_Classification w/ Convolutional Neural Network

### Author : Gukhwan Hyun

 * [Introduction](#introduction)
 * [Dataset](#dataset)
 * [Models](#model)
 * [Conclusion](#conclusion)  
  

# Introduction
COVID-19의 합병증으로 폐렴이 보고되었다. 백신, 방역지침 등에도 불구하고, 변이를 일으키며 끝을 모르고 퍼져나가는 COVID-19 덕분에 의료시스템은 붕괴와 유지 사이에서 아슬아슬한 줄타기를 하고있다. 따라서, 나는 X-Ray 사진을 정상과 폐렴으로 구분하는 모델을 설계하여, 인공지능 모델을 통해 의사의 업무를 보조할 수 있는지 알아보고자 한다. 


# Dataset
실험에 사용된 데이터는 중국 광저우 의료 센터의 1~5살 사이의 소아 환자들로부터 수집되었다. 

데이터셋은 2090x1858x1 크기를 가지는 총 5856장의 X-Ray 사진으로 구성되어있으며, 정상과 폐렴의 비율은 약 1:2 정도로 폐렴 사진이 2배가량 많았다.

(To read more about, visit -> https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia) 


# Model
모델 설계는 2가지 방법을 시도하였다. 
* 첫번째는 커스텀 모델로 LeNet 구조를 기반으로 Convolution Layer, Filter, Fully Connected Layer의 숫자에 따라 정확도가 얼마나 달라지는 지 확인하였다. 또한 Data augmentation을 통해 데이터 숫자를 늘려 Overfitting을 줄이고자 하였다.

* 두번째는 VGG-19 구조를 기반으로 이미지 분류를 진행하였다. 


## 1st_model
Convolution Layer가 적을수록, 필터와 밀집층의 갯수는 증가할수록 높은 정확도를 보였다.

훈련데이터, 테스트데이터의 정확도(accuracy)는 각각 99.6%, 72.4%로 모델이 데이터에 과적합(overfitting)을 보였다.
테스트 데이터에서 폐렴사진에 대한 재현율(sensitivity)이 100% 으로 실제 폐렴 사진을 모두 구분해내어 신뢰성을 가지나, 정밀도는 69% 정도로 실제 상황에서 의사를 보조하기에는 다소 부족해보였다. 

## 1st_model w/ data augmentation
정상 X-ray 숫자가 부족이 정밀도가 낮은 원인이 아닐까 생각되어 추가적인 데이터를 얻고자 했다. 기존의 데이터가 사전에 의사의 검증을 거친 퀄리티가 높은 사진이었기에 다른 소스에서 비슷한 수준의 이미지를 얻기가 쉽지 않다고 생각되어, ImageDataGenerator 를 이용하여 가상의 데이터셋을 추가하였다. 

그 결과, 테스트 데이터에서 정확도 87.3%, 재현율 94%, 정밀도 87% 로 여전히 완벽하지는 않지만 기존 모델에 비해 보조수단으로써의 가치가 상승되었다.   


## 2nd_model - pre_trained VGG19 
커스텀 모델에는 한계가 있다고 생각하여, 이미지 분류로 업계에서 검증된 모델 중 하나인 VGG-19 모델을 기반으로 이미지 분류를 진행하였다.

다른 이미지들로 사전학습된 모델을 사용하는 것이기 때문에, 특성 정보의 소실이 불가피하게 생길 수 있다고 판단되어, 2개의 FC 층을 추가하여 구조의 변화를 주었다. 

그 결과, 테스트 데이터에서 정확도 87%, 재현율 98%, 정밀도 84%로 data augumentation을 사용한 커스텀 모델과 비슷한 결과를 보였다. 


# Conclusion
이미지 분류에서 CNN 모델은 Convolution Layer가 적을수록, 필터와 밀집층의 갯수는 증가할수록 높은 정확도를 보였다.
또한 학습 조건에서 차이가 있어 확신을 가지긴 어렵지만, 데이터의 숫자를 늘리는 것과 네트워크의 깊이를 깊게하는 것은 결과에 비슷한 영향력을 끼친다는 것을 
알 수 있었다. 

