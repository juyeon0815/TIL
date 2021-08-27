# CNN

## 🤔CNN이란?

- Convolutional Neural Networks의 약자
- 딥러닝에서 이미지나 영상 데이터를 처리할 때 사용

### 👉🏻왜 CNN을 사용할까?

- DNN의 문제점을 해결하기 위해서

---

❓ DNN이란?

- 입력층과 출력층 사이에 여러 개의 은닉층들로 이루어진 인공신경망

    ![stun](/res/DNN.png)

- DNN은 1차원 형태의 데이터를 사용하는데, 2차원의 이미지가 입력값이 되는 경우, 1차원인 데이터로 만드는 과정에서 이미지의 공간적/지역적 정보가 손실
- 추상화과정 없이 바로 연산과정으로 넘어가 버리기 때문에 학습시간과 능률의 효율성 저하

⭐ 이러한 DNN의 문제점을 해결하기 위해서 CNN 사용!

⇒ CNN은 이미지를 그대로 받음으로써 공간적/지역적 정보를 유지한 채 특성들의 계층을 빌드업

⇒ CNN은 이미지 전체보다는 부분, 이미지의 한 픽셀과 주변 픽셀들의 연관성 살리기

![stun](/res/cat.png)

- 이미지가 주어졌을 때 이 이미지가 고양이인지 아닌지 판단할 수 있는 모델을 만들고 싶을 경우에는 고양이의 주요 특징을 잡아 구분할 수 있다.
- 전체 이미지를 보는 것보다는 구별할 수 있는 주요 특징을 잘라서 본다면 훨씬 더 효율적이다.

⭐ 이것이 CNN!!!

### 👉🏻CNN의 구성 layers

1. Convolution의 layer
    - Convolution이란? : input이 주어졌을 때, filter의 사이즈 만큼 데이터를 보고 input 데이터와 filter에 대응하는 것을 곱하여 다 합친 것을  output에 배치하는 operation

        ![stun](/res/convolution.png)

    - 데이터의 특징을 추출하는 과정으로 데이터의 특징을 파악하고 파악한 특징을 한장으로 도출시키는 과정

2. Pooling layer
    - Convolution 과정을 거친 레이어의 사이즈를 줄여주는 과정 ( Max Pooling )

    ![stun](/res/pooling.png)

3. Activation function

    ![stun](/res/activation.png)

1. Fully Connected layer
    - Convolution - Pooling - ReLU 를 통해 스택을 쌓고 최종적으로 Fully Connected layer을 통해 하나의 값으로 만들어 준다.

### 👉🏻CNN이 성능이 좋은이유

- 계층적 특징 표현하는 방법을 배우더라.
- Convolution 레이어의 적층을 통해 자연스럽게 유도된 특징을 갖는다.

### 👉🏻CNN알고리즘

1. AlexNet
    - Conv - Pool - LRN - Conv - Pool - LRN - Conv - Conv - Conv - Pool - FC -FC -FC

    ![stun](/res/alexNet.png)

    - LRN ( Local Response Normalization) : Activation 억제, 흥분된 뉴런의 주변 정규화 → Batch Normalization을 사용하면 훨씬 더 좋은 성능과 안정적인 학습가능

2. VGGNet 
    - AlexNet 보다 더 깊은 아키텍처 ( 16 ~ 19 layers )
    - 간결한 아키텍처 ( LRN 없어짐, 3X3 conv filters, 2X2 max pooling만 사용 )
    - 더 좋은 퍼포먼스 ( AlexNet보다 획기적으로 좋은 성능을 보임 )
    - 더 좋아진 일반화 성능 ( Fine tuning 없이 다른 방법으로 일반화 )

    ---

    ⭐ 더 많은 layer를 쌓으려고 했지만 네트워크가 깊어짐에 따라, 정확도가 더 빠르게 수렴하지만 성능이 나빠지는 결과 확인 ⇒ 최적화 문제!!!!!!!

3. ResNet
    - VGGNet의 최적화 문제를 어떻게 해결할까에서 등장
    
      

참고자료

[https://halfundecided.medium.com/딥러닝-머신러닝-cnn-convolutional-neural-networks-쉽게-이해하기-836869f88375](https://halfundecided.medium.com/%EB%94%A5%EB%9F%AC%EB%8B%9D-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-cnn-convolutional-neural-networks-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-836869f88375)