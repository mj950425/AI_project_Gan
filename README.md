![image](https://user-images.githubusercontent.com/52944973/104883289-e5845e80-59a7-11eb-995c-b69eda1128c8.png)

요즘 GAN 모델이 핫하니깐 관련 프로젝트를 찾아보았는데, Personal 시대를 맞이해서 개인 손글씨를 폰트로 만든다면 좋을 것 같아 프로젝트를 진행하게 되었습니다!

![image](https://user-images.githubusercontent.com/52944973/104883326-f634d480-59a7-11eb-86ce-14aab6754642.png)


최종 목표입니다 ㅎㅎ..




한글폰트를 생성하기 위해서 모델은 총 세단계의 과정을 거칩니다. 

첫번째로 프리트레이닝 과정에서는 컴퓨터 폰트 27종을 통해 글자의 특징을 추출하고 복원하는 것을 학습합니다. 이후 개인의 손글씨 210자 를 프리트레인모델을 파인튜닝하여 학습시킵니다. 파인튜닝을 통하여 특징 추출 및 복원을 학습한 모델은 학습하지 않은 나머지 2224자를 생성할 수 있게 됩니다. 이 과정을 인퍼링이라고 합니다.

![image](https://user-images.githubusercontent.com/52944973/104883522-3b590680-59a8-11eb-9d20-4891e2f61b63.png)

Unet구조를 가지는 pix2pix모델을 사용했습니다||_##]

Unet구조를 통해서 특징 Z를 잘 뽑아내고 Fake의 Z와 Source의 Z를 다시 인코더에 넣어서 비교하는 Constant loss 그리고 글자 폰트 카테고리를 비교해주는 Category loss와 Fake이미지와 Ground Truth이미지와의 L1거리를 loss텀으로 추가해서 모델을 만들었습니다.

![image](https://user-images.githubusercontent.com/52944973/104883527-3eec8d80-59a8-11eb-92e9-4519abfea1b9.png)

기술의 문제점으로는 프리트레인 과정에서 글자들의 디테일한 부분을 잘 잡아내지 못하고 어려운 글자들을 복원하지 못한다는 점이었습니다.

![image](https://user-images.githubusercontent.com/52944973/104883529-40b65100-59a8-11eb-8126-6a11bb8047cc.png)

다양한 논문들을 통해서 개선방안을 모색했습니다. 대표적으로 Spectral Normalized Gan과 Self-attention Gan 그리고 Super resolution Gan을 추가했습니다.

![image](https://user-images.githubusercontent.com/52944973/104883535-43b14180-59a8-11eb-8b7f-e16d92270571.png)

모델의 구조 또한 논문의 내용을 바탕으로 여러가지 loss텀을 추가하면서 변화를 시도했습니다. 우선 학습 과정에서 시간이 너무 오래걸려서 이미지의 픽셀을 줄인 뒤 출력 이미지의 해상도를 SR GAN으로 높여주는 방식을 택했습니다. 모델에 어텐션과 정규화 부분의 방식을 바꿈으로서 좀 더 나은 결과를 확인할 수 있었네요

![image](https://user-images.githubusercontent.com/52944973/104883541-457b0500-59a8-11eb-8bb4-fbbb680a664f.png)
최종 결과물

학습 과정에서 최적의 하이퍼 파라미터와 최적의 모델 구조를 찾는데 아주 많은 시간이 들어 힘이 들었네요..

아주 뛰어난 결과는 아니지만 어느정도 글씨체를 닮은 것 같네요^^


