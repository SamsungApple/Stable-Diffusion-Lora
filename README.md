# Stable-Diffusion-Lora 학습 환경 세팅 및 학습 방법 정리

본 Repository는 [the repository maintained by kohya-ss](https://github.com/kohya-ss/sd-scripts)와 [루리웹의 글](https://bbs.ruliweb.com/community/board/300143/read/59967569)을 참고해서 Lora 모델 학습을 진행한 방법을 정리한 글입니다.
kohya-ss님과 글을 작성해 주신 루리웹 회원분께 감사드립니다.

기본적으로 https://github.com/kohya-ss/sd-scripts의 글의 진행 방법과 비슷하지만 일부 수정되어 있습니다.
Base 코드는 https://github.com/kohya-ss/sd-scripts에서 시작됩니다.

## 작업환경
* Ubuntu 20.04 (리눅스)
* Docker
* CPU : Ryzen 9 5900X
* RAM : 48GB
* GPU : Nvidia RTX 3090

## 기본 학습 환경 세팅
1. Anaconda Docker Image 다운로드 및 컨테이너 생성 진행
2. 생성한 컨테이너 접속
3. Python 3.10 버전의 Anaconda 가상환경 세팅
   ```
   conda create -n (아나콘다 가상환경 이름) python=3.10
   ```
4. ``` 
   git clone https://github.com/kohya-ss/sd-scripts.git
   cd sd-scripts 
   ```
5. pytorch 1.13.1 버전 설치
   ```
   conda install pytorch torchvision torchaudio pytorch-cuda=11.6 -c pytorch -c nvidia
   pip install --upgrade -r requirements.txt
   ```
6. xformers 설치
   ```
   pip install xformers==0.0.17.dev473
   ```
7. 설치 및 동작과정에서 opencv-python 라이브러리 관련 오류가 있을 수 있음
   아래의 코드를 실행
   ```
   pip uninstall opencv-python
   pip install opencv-contrib-python-headless==4.7.0.72
   ```
8. accelerate config 설정
   ```
   accelerate config
   ```
   질문에 대해서는 아래와 같이 진행합니다.
   ```
   - This machine
   - No distributed training
   - NO
   - NO
   - NO
   - all
   - fp16
   ```
   
## Credits
[khoya-ss's repo](https://github.com/kohya-ss/sd-scripts)와 [루리웹 글](https://bbs.ruliweb.com/community/board/300143/read/59967569)을 참고 및 활용하였습니다. Repository를 작성해주신 khoya-ss님과 루리웹 회원분께 감사드립니다.
공부하는데 큰 도움을 받았습니다.

## 주의(?)
Lora 모델 학습을 위해 사용한 데이터 수집과 데이터에 대한 설명은 요청을 주셔도 따로 말씀드리지 않을 것이며
학습 데이터 및 학습된 모델의 공유 또한 하지 않을 것입니다.
본 Repository는 학습 환경 세팅 및 공부의 목적으로 만들었습니다.




















