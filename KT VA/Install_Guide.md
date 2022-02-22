# KT VA Install Guide

## Install File
* HH03_20210104.tar : For CentOS 6.7
* HH03_20210104.tar : For CentOS 7.x
* lib_new.tar.gz : Library for CentOS 7.x
---

## Install progress
### Package file copy and decompression
``` shell
>>> mv [install_package].tar /data/3rd_va/www
>>> cd /data/3rd_va/www
>>> tar -xf [install_package].tar
>>> tar -xf 3rd_va_1.3.2_release.tar
>>> tar -xf 3rd_lib_1.3.1_release.tar
```
---
### Run script
``` shell
>>> cd /data/3rd_va/www/3rd_va_1.3.2.release
>>> ./0_setup.sh [network_interface_name]
>>> cat application.properties
```   

* ifconfig 명령어를 통해 network interface name 확인 후 직접 입력하여 Script 실행
* 0_setup_new.sh : CentOS 7.x 
* application.properties 아래의 문자열이 변경되었는지 확인
  * __int-host
  * __va-vip
  * __node_name
  * __node_ip
  * __net_if
  * __int-host, __va-vip : /etc/hosts
* consul.json 수정
  * __node_ip, __node_name 정보 확인
  * retry_join 값이 원형으로 클러스터링 되어 있는 서버의 IP 값을 확인하여 전, 후 서버 IP 값을 입력
  * 리더가 되는 서버의 경우 bootstrap 값을 true로 하고, 나머지 저버는 false로 수정
  * va_platform_install.sh 실행
    ``` shell
    >>> ./va_platform_install.sh
    ``` 
  * 설치 후, /data/3rd_va  폴더에 아래와 같이 bin, lib, script 폴더가 생성 확인

---
### 설치 후 작업 내용
* jq 실행 권한 추가
  ``` console
  >>> chmod +x /deta/3rd_va/bin/jq
  ```

* crontab 수정
  ``` console
  >>> crontab -e
  @reboot ~/va/3rd_va/script/ivx_delete_image.sh > /dev/null 2 > &1
  ```
  기존에는 crontab에 'LD_LIBRARY_PATH=/data/3rd_va/lib'를 입력.   
  그러나, 타사 Library와의 충돌로 vaplatform.sh 에서 LD_LIBRARY_PATH를 설정.   
  현재 가지고 있는 스크립트는 최신 버전이 아니므로 해당 사항 확인 필요

* source ~/.bash_profile
---
### 실행 방법
* 리더 서버 실행
  ``` console
  >>> cd /data/3rd_va/bin
  >>> ./consul.sh start
  >>> ./vaplatform.sh start
  ```
* 리더 서버의 VA Manager가 정상적으로 실행되었는지 확인(gigasurv 확인)
  ``` console
  >>> ps -ef | grep java
  ```
* consul이 정상적으로 실행되었는지 확인
  ``` console
  >>> consul members
  ```