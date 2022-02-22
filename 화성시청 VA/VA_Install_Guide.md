# 화성 VA Install Guide
## VA 설치
* 설치 파일 복사
  ``` console
  >>> cd /home/vasvc
  >>> mkdir install
  >>> cd install
  ```
  /home/vasvc/install 폴더로 va_install_20210325.zip 복사
  ``` console
  >>> unzip va_install_20210325.zip
  ```

* 사용할 폴더 생성 및 권한 변경
  ``` console
  >>> sudo mkdir -p /svc/vasvc/
  >>> sudo chown -R vasvc:vasvc /svc/vasvc
  >>> sudo mkdir -p /logs/vasvc/
  >>> sudo chown -R vasvc:vasvc /logs/vasvc
  ```

* Library 설치
  ``` console
  >>> cd /home/vasvc/install
  >>> unzip Ubuntu_18.04_lib_install_20210111.zip
  >>> cd 1.python/; chmod +x install.sh; ./install.sh; cd ..
  >>> cd 4.gcc/; chmod +x install.sh; ./install.sh; cd ..
  >>> cd 5.g++/; chmod +x install.sh; ./install.sh; cd ..
  >>> cd 6.make/; chmod +x install.sh; ./install.sh; cd ..
  >>> cd 7.curl/; chmod +x install.sh; ./install.sh; cd ..
  ```

* 분석 프로그램(Manager, Process) 파일 복사 및 권한 변경
  ``` console
  >>> cp -rf intellivix /svc/vasvc
  >>> cd /svc/vasvc/intellivix
  >>> ln -s processes/application.properties application.properties
  >>> chmod +x Intellivix vaplatform.sh watchdog.sh run_hs.sh va_reboot.sh kill_intellivix_using_ssh.sh
  >>> chmod +x check_process.sh nasdata_delete.sh
  >>> cd /svc/vasvc/intellivix/jdk1.8.0_191/bin
  >>> chmod +x *
  >>> cd /svc/vasvc/intellivix
  >>> tar -xvf lib_ubuntu.tar
  >>> rm -rf lib_ubuntu.tar
  ```

* Intellivix(Process) Library link 설정
  ``` console
  vi /home/vasvc/.profile

  # 아래 구문 추가 후 저장
  export LD_LIBRARY_PATH=/svc/vasvc/intellivix/lib:$LD_LIBRARY_PATH

  source /home/vasvc/.profile
  ```

* Manager Option 설정
  ``` console
  vi application.properties

  # 아래의 값을 서버 설정에 맞게 수정
  ap_server_index
  node.name
  network.interface
  dnn.server.url
  ```

* crontab 설정
  ``` console
  crontab -e

  # 아래 구문 추가 후 저장
  */15 * * * * /svc/vasvc/intellivix/check_process.sh
  ```
  nasdata_delete.sh 은 전 서버에 설정할 필요 없음.   
  단, 구버전 VA(40.10.15.21 ~ 48)과 신규 VA(49 ~ 60)가 바라보는 NAS 폴더가 다르므로 각 그룹별로 필요에 맞게 설정할 것.   
  * 예제
    ``` console
    >>> 0 1 * * * /svc/vasvc/intellivix/nasdata_delete.sh 02001 03000 &>/dev/null &
    ```

* NAS 폴더에 Process 가 사용할 폴더 생성
  ``` console
  >>> cd /nasdata
  >>> mkdir Meta
  ```
---
## VA 자동실행 관련 추가 설치
### 자동 실행 관련 추가 설치가 필요한 이유
  * Intellivix(Process)가 Update 되면서 Ubuntu 18.04 OS에서 실행 시, 약 150여개 채널 이상 동작하지 않는 문제 있음.
  * 이를 해결하기 위해 vasvc2 계정을 생성하여 vasvc, vasvc2 두 개 계정을 사용하여 동작하도록 시나리오가 변경 됨.
  * 서버가 부팅 후, 자동 실행시 ssh를 통해 두개의 manager를 실행시켜서 채널 문제를 해결하도록 한다.

### vasvc2 계정 생성 및 vasvc2에 VA 설치 폴더 생성
```console
>>> sudo adduser vasvc2
>>> sudo gpasswd -a vasvc2 vasvc
>>> sudo gpasswd -a vasvc vasvc2
>>> sudo mkdir -p /svc/vasvc2
>>> sudo chown -R vasvc2:vasvc /svc/vasvc2
>>> sudo mkdir -p /logs/vasvc2
>>> sudo chown -R vasvc2:vasvc /logs/vasvc2
```

### root 계정을 사용할 수 있도록 비밀번호 변경 및 root 접속
``` console
>>> sudo passwd root
>>> su -
```

### SSH 사용 시, 인증키를 사용하여 동작하도록 설정
``` console
>>> sudo mkdir -p /root/.ssh
>>> sudo chmod 700 /root/.ssh
>>> cd /root/.ssh
>>> sudo ssh-keygen -t rsa
>>> 
>>> cp id_rsa.pub authorized_keys
>>> chmod 600 authorized_keys
>>> 
>>> sudo mkdir -p /home/vasvc/.ssh
>>> sudo chmod 700 /home/vasvc/.ssh
>>> sudo chown vasvc:vasvc /home/vasvc/.ssh
>>> sudo cp authorized_keys /home/vasvc/.ssh/
>>> sudo cp id_* /home/vasvc/.ssh
>>> chown vasvc:vasvc /home/vasvc/.ssh/*
>>> 
>>> sudo mkdir -p /home/vasvc2/.ssh
>>> sudo chmod 700 /home/vasvc2/.ssh
>>> sudo chown vasvc2:vasvc /home/vasvc2/.ssh
>>> sudo cp authorized_keys /home/vasvc2/.ssh/
>>> sudo cp id_* /home/vasvc2.ssh
>>> chown vasvc2:vasvc /home/vasvc2/.ssh/*
```

### 자동 실행 되도록 설정
``` console
>>> su - vasvc
>>> sudo vi /etc/rc.local

# 아래 구문 추가 후 저장
#!/bin/bash
/svc/vasvc/intellivix/va_reboot.sh
exit 0

>>> sudo chmod +x /etc/rc.local
>>> sudo vi /lib/systemd/system/rc-local.service

# 아래 구문 추가 후 저장
[install]
WantedBy=multi-user.target

>>> sudo systemctl enable rc-local.service
```

### vasvc 계정에 설치 파일을 vasvc2 쪽으로 복사
``` console
>>> cd /svc/vasvc
>>> sudo cp -ar intellivix /svc/vasvc2/
>>> sudo chown -R vasvc2:vasvc /svc/vasvc2/intellivix
```

### vasvc2 계정 Library 링크 설정
``` console
>>> su - vasvc2
>>> vi /home/vasvc2/.profile

# 아래 구문 추가 후 저장
export LD_LIBRARY_PATH=/svc/vasvc2/intellivix/lib:$LD_LIBRARY_PATH

>>> source /home/vasvc2/.profile
```

### manager option 설정
``` console
>>> cd /svc/vasvc2/intellivix
>>> vi application.properties

# 아래 내용 확인, 수정 후 저장
logging.file : /logs/vasvc2/vamanager/applog/manager/manager.log
server.port=8081
dnn.server.url : (필요에 따라 변경)
camera.first.index 130
camera.max.count 135
manager.config.path: /svc/vasvc2/intellivix/processes
va.process.path: /svc/vasvc2/intellivix/Intellivix

>>>
```

### 스크립트 파일 경로 수정 및 불필요한 파일 삭제
``` console
>>> vi check_process.sh
>>> vi vaplatform.sh
>>> vi watchdog.sh
# 변경 : /svc/vasvc -> /svc/vasvc2

>>> rm -f run_hs.sh va_reboot.sh kill_intellivix_using_ssh.sh nasdata_delete.sh
```

### crontab 설정
``` console
>>> crontab -e

# 아래 구문 추가 후 저장
*/15 * * * * /svc/vasvc/intellivix/check_process.sh
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