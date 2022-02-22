# VisionAI Install Guide

## VisionAI 설치
---
### 설치 전 준비사항
* NVIDIA Graphic Driver(NVIDIA-Linux-x86_64-430.40.run)
* CUDA Driver(cuda_10.1.168_418.67.run)
---
### 설치 파일 복사
``` console
>>> cd /home/vasvc
>>> mkdir install
>>> cd install
```
/home/vasvc/install 폴더로 vision_ai_install_20210325.zip 복사
``` console
>>> unzip vision_ai_install_20210325.zip
```
---
### 사용할 폴더 생성 및 권한 변경
``` console
>>> sudo mkdir -p /svc/vasvc/
>>> sudo chown -R vasvc:vasvc /svc/vasvc
```
---
### Cudnn, terserRT 설치
``` console
# Cudnn
>>> cd /home/vasvc/install/driver
>>> tar -xvf cudnn-10.1-linux-x64-v7.6.3.30.solitairetheme8
>>> cd cuda
>>> sudo cp -ar include/* /usr/local/cuda/include
>>> sudo cp -ar lib64/* /usr/local/cuda/lib64

# tensorRT
>>> cd /home/vasvc/install/driver
>>> tar -xvf TensorRT-6.0.1.5.Ubuntu-18.04.x86_64-gnu.cuda-10.1.cudnn7.6.tar.gz
>>> cd TensorRT-6.0.1.5
>>> sudo cp -ar include/* /usr/local/cuda/include
>>> sudo cp -ar lib/* /usr/local/cuda/lib64
```
---
### VisionAI 파일 복사
``` console
>>> cd /home/vasvc/install
>>> cp -r VisionAI /svc/vasvc/
>>> cd /svc/vasvc/VisionAI/
>>> tar -xvf linux_lib_ubuntu_18_04.tar
>>> rm -rf linux_lib_ubuntu_18_04.tar
>>> chmod +x VisionAI.Process visionai_run.sh watchdog.sh
```
---
### Library link 설정
``` console
vi /home/vasvc/.profile

#아래 구문 추가 후 저장
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:/svc/vasvc/VisionAI/linux_lib:$LD_LIBRARY_PATH

source /home/vasvc/.profile
```
---
### 자동 실행 설정
``` console
crontab –e

#아래 구문 추가 후 저장
@reboot /svc/vasvc/VisionAI/visionai_run.sh start
```
---
### 프로그램 실행 후 TRT 파일 생성
``` console
./VisionAI.Process

# 실행 시 수 분 간 trt 파일 생성을 진행한다.
# 생성 완료 후 프로그램이 자동으로 종료 된다.
# /svc/vasvc/VisionAI/DNNDataFiles 경로 안에 .trt 파일이 3개가 보여야 한다.

```
---
### 옵션 설정
-	VisionAI가 처음 실행될 때 ApplicationSettings.json 파일이 생성된다.
-	해당 파일은 VisionAI 옵션 설정파일 이다.
``` console
vi ApplicationSettings.json
# Server.sessionTimeoutMil 값을 86400000 으로 변경한 후 저장한다.
```
---
## 프로그램 실행 및 종료 방법
### 실행
``` console
>>> cd /svc/vasvc/intellivix
>>> ./run_hs.sh start
```

### 종료
``` console
>>> ./run_hs.sh stop
```