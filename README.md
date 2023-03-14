# Stable-Diffusion-Lora

해당 Repository는 [the repository maintained by kohya-ss](https://github.com/kohya-ss/sd-scripts)와 [루리웹의 글](https://bbs.ruliweb.com/community/board/300143/read/59967569)을 참고해서 Lora 모델 학습을 진행한 방법을 정리한 글입니다.
kohya-ss님과 글을 작성해 주신 루리웹 회원분께 감사드립니다.

기본적으로 https://github.com/kohya-ss/sd-scripts의 글의 진행 방법과 비슷하지만 일부 수정되어 있습니다.

## 작업환경
* Ubuntu 20.04
* Docker
* CPU : Ryzen 9 5900X
* RAM : 48GB
* GPU : Nvidia RTX 3090

## 세팅
1. Anaconda Docker Image 다운로드 및 컨테이너 생성 진행
2. 생성한 컨테이너 접속
3. Python 3.10 버전의 Anaconda 가상환경 세팅
4. 
  ``` git clone https://github.com/kohya-ss/sd-scripts.git
   cd sd-scripts ```
