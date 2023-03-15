## Lora 모델 학습을 위한 방법 정리
* (학습에 사용되는 파라미터 등에 대한 공부는 아직 필요함)
* 공부하는 내용대로 내용을 추가할 예정
* Prompt를 활용하여 학습하는 방법에 대한 내용은 추후 공부하여 작성 예정

#### 1. Readme.md의 내용대로 진행하면 Lora 모델 학습을 위한 환경 세팅 됨.

#### 2. 모델 학습을 위한 데이터를 준비

#### 3. 데이터 학습을 위한 폴더 구조는 아래와 같이 준비 (https://bbs.ruliweb.com/community/board/300143/read/59967569 글을 참고함)
```
Train
- img (학습에 사용할 이미지가 들어 있는 경로)
  - reg_[base prompt] (Regualrization 이미지, 아직 해당 데이터의 역할에 대한 공부 필요....)
    - 반복횟수_[base prompt] (반복횟수 등에 대한 내용은 공부 필요)
  - train_[임의] (학습에 사용될 기본 데이터 있는 폴더)
    - 반복횟수_[use prompt] [base prompt] (반복횟수 등에 대한 내용은 공부 필요)
- model (모델이 저장되는 경로)
```
위 반복 횟수와 관련된 내용은 아직 확인 필요, epoch/step과 관련된 것은 학습 코드에 추가함.

#### 4. Docker 컨테이너 및 Anaconda 가상환경 접속 후 코드가 있는 경로로 이동
```
~ 컨테이너 및 가상환경 접속
./sd-scripts
```

#### 5. 아래의 코드를 bash 파일로 생성하여 모델 학습 진행
```
accelerate launch --num_cpu_threads_per_process 1 train_network.py 
--pretrained_model_name_or_path=(Stable Diffusion Model Weight 경로)
--output_dir=(학습된 모델이 저장될 경로)
--output_name=(학습된 모델이 저장될 이름)
--save_model_as=safetensors (Weight 저장 포맷명)
--prior_loss_weight=1.0 
--max_train_steps=4800
--learning_rate=1e-4 
--optimizer_type="AdamW" (권장은 AdamW8bit으로 되어있지만 오류가 있는지 동작하지 않아 AdamW로 설정함) 
--mixed_precision="fp16" 
--cache_latents 
--gradient_checkpointing 
--save_every_n_epochs=10 (학습된 모델이 몇 epoch 마다 저장될지 설정, 1이 아니면 첫 epoch에 모델은 저장되지 않는다)
--network_module=networks.lora (Lora 모델을 학습하는 경우 networks.lora로 작성해야함)
--resolution=1024,1024 (모델을 학습할 해상도, enable_bucket이 되어 있으면 해상도를 임의로 나눠서 학습이 진행됨)
--clip_skip=2 
--reg_data_dir=(reg_[base prompt] 경로)
--train_data_dir=(train_[임의] 경로)
--enable_bucket 
--xformers 
```

#### Lora 모델이 저장되는 것을 확인할 수 있다.

---
### 추가 내용들
--mixed_precision="fp16"이 아닌 --mixed_precision="no"로 설정하면 학습 시간이 배 이상으로 늘어난다.(2시간 40분 -> 8시간 X분으로 늘어나는 것 확인) 
