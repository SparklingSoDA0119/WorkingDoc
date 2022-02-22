# LGU+ VA
## Git Server
* VA Process
  * http://172.16.4.99/administrator/VAProcess_VS.git
  * Branch : VAProcess_LG
* VA Manager
  * http://172.16.4.99/administrator/VAManager.git
  * Branch : master
* Dnn Process
  * http://172.16.4.99/administrator/SI_Project.git
  * Branch : dnn_lg
* Dnn Manager
  * http://172.16.4.99/administrator/VAManager.git
  * Branch : DnnManager
* FileRelayServer
  * http://172.16.4.99/administrator/SI_Project.git
  * Branch : dnn_lg
  * LabelingTool/
* VATestScheduler
  * http://172.16.4.99/administrator/IntelliVIX_iNVR.git
  * Branch : Develop(Face)_newMerge_x64
  * Projects/External link/VATestScheduler/
---
---
## 인수인계 문서 설명
* LG U+/DnnManager & Process.dock(/.pdf)
  * DNN 서버 설치 문서
  * DNN_Server_Install.zip 로 설치 진행
  * 요약
    * Install (사전에 DNN_Server_Install.zip 복사해야 함.)
    ```command
    >>> mkdir ~/LGUplus/install
    >>> cd ~/LGUplus/install
    >>> cp -rf ~/DNN_Server_Install.zip .
    >>> unzip DNN_Server_Install.zip
    >>> cd DNN_Server_Install
    >>> chmod +x dnn_server_install.sh
    >>> ./dnn_server_install.sh
    # 설치 진행중, 정상적이지 않은 경우 ctrl + c를 눌러 동작을 중지시킴
    ```
  * 그 외 문서 참조.   
---
      
* 20200706_이벤트검출서버_객체검출서버_AND-03_연동규격서_v1.2.dock
  * VA 와 DNN 에서 사용되는 Interface 규격서
---

* 2018_0816_학습플랫폼_v0.2.pptx
  * 학습 플랫폼 관련 문서.
  * FileRelayServer와 관련은 없으나, 인수인계에 포함함.
---
* smf구조_fix.doc
  * Stream Meta File
  * FileRelayServer에서 Read / Write 하는 smf 파일 구조
  * 
---
* 파일중계서버 흐름도.pptx
  * 현재와는 다름.
  * **현재는?**
---
* 파일중계서버_운영자매뉴얼.docx
  * FileRelayServer 매뉴얼
---
* 파일중계서버_운영자매뉴얼.docx
  * FileRelayServer install and management manual.
---
* 학습도구 중계서버 인터페이스 설계서_v0.1.docx
  * FileRelayServer에서 REST API 규격서
---
* 20200810_VSaaS_VA서버_연동규격서_v0.25.docx
  * VA 3종 적용 시, 연동 규격서
  * **VA 3종 이란?**
---
* Linux_Server_Manager_설계_v0.1_200618.pptx
  * VAManager consul 관련 설명이 작성된 문서
  * **consul 이란?**
---
* VA Manager to VA Process Interface_v1.1LGU+ 개발 변경.xlsx
  * VAManager와 Process 간 Interface 정의서
---
* VA_Manager_상태확인가이드.docx
  * VAManager를 consul 명령어를 통해 상태 체크를 할 수 있는 문서
---
* VA_Platform_Install_Guide.docx
  * 상용 설치를 진행한 설치 가이드 문서로 VA_Platform_Install.zip 파일로 설치 진행
  * 최초 설치시에만 사용하고, 이후에는 LGU+에서 제공한 업데이트 스크립트로 변경된 부분만 업데이트 진행.
---
* 시험 스케쥴러 User Guide 1.0.2.docx
  * VATestScheduler 사용 가이드 문서
    * 박찬호 부장이 추가한 DNN Process 테스트 기능은 문서에 없음.
---
---

## Appendix
* Dnn과 VA 실행 Script인 vaplatform.sh 파일의 내용이 상용과 다를 수 있음.
  * 로그 쌓이는 문제로 현장에서 내용 수정 : /dev/null 로 Log 출력

* FileRelayServer는 본래 LabelingTool 작업 때, 부속 프로그램으로 들어가서 Rest 요청 시, 해당 파일을 sftp로 전달하였음
  * 현재 사용하지 않음.
  * 박찬호 부장이 내부적으로 LG 영상 반출 시, mp4로 저장하는 기능만 사용함.

* VA 3종 작업 내용이 VATestScheduler에 반영되지 않아 VAProcess 테스트 기능은 현재 최신버전에서 동작하지 않음.
  * **최신버전에서 사용하려면 어떻게 해야함?**

* 20211022_115445_이병천_부장(팀장)_융합개발팀_인텔리빅스_(windowsbc@intellivix.com)_FW__[U+_지능형CCTV].eml
  * VA Process에서 Event 발생 시, VA Manager로 메시지를 전송함.
  * 그러나, 수신 Logic이 없음.(System 함수로 curl 명령어를 전달하는 구조)
  * 추가 개발 요청이 들어올 수 있음.

* 20220211_175106_양재영_선임_(jaeyoungyang@lguplus.co.kr)_Re__RE__[유플러스]_DNN서버_NullPointmail.eml
  * DNN 서버 NullPointer Exception 장애 대응 결과

* 20220217_160745_최윤경_(ykchoi@intellivix.com)_FW__[자료_요청]_VA_manager__-__VA_mail.eml
  * VA Process에서 VA Manager로 전송하는 Message 규격


## Spec
* OS : Oracle Linux 7.4
* JDK Version : 1.8.0_191
* CUDA Version : 10.1.168_418.67_linux


