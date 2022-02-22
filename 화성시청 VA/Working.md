## 화성시청 VA
---
---

## Gitserver
* VA Server
  * http://172.16.4.99/administrator/VAManager.git
  * Branch : VAManager_hs

* VA Process
  * http://172.16.4.99/administrator/VAProcess_VS.git
  * Branch : VAProcess_HS

* VisionAI
  * http://172.16.4.99/administrator/VisionAIServer.git
  * Branch : master

---
## 문서 설명
* application properties 추가된 옵션 설명.txt
  * 최신 화성 진행 중, 추가된 Manager 옵션 설명

* 화성 Manager 동작 시나리오.pptx

* 화성 새로 추가된 VA 스크립트 설명.txt
  * 화성에서 새로 추가된 스크립트에 관한 설명
  * 기존과 다르게 2개의 계정으로 운영되므로 확인 요망

* 분배서버 연동 인터페이스_20200514.pptx
  * 분배서버로 전달하는 메시지가 변경된 내용이 포함된 문서

* IntelliVIX-Vision_API_연동규격_v1.0_20200420.xlsx
  * From. 오범석 수석

* VisionAI-SourceFiles.xlsx
  * From. 오범석 수석

* VA와 Vision-AI 연동 정보.xlsx
  * 실제 화성 현장에 VA와 Vision-AI 연동 정보를 작성한 문서

* 선별PW변경.xlsx
  * CUDO 조장연 차장이 공유한 화성 현장 서버별 패스워드 문서

* 화성 이슈 정리.docx
  * 주요 이슈 정리

* 문서/김영재주임 작업내용/*.txt
  * VisionAI 설치 외근 시 진행 내용. From.김영재 주임

* 화성 VA 설치 및 실행 매뉴얼.docx

* 화성 VisionAI 설치 및 실행 매뉴얼.docx

* 서버 점검.docx
  * CUDO 의 서버 점검 요청 시, 확인 내용을 작성한 문서

* 화성_DB_SystemConfig 연계문서.xlsx
  * CCTV_INFO 테이블과 SystemConfig.xml 파일 내, 태그 값 연계 정보

* 화성시 PTZ Camera영상 분석을 위한 방안 (구성 및 흐름도).pptx
  * PTZ 카메라 분석 시, PTZ 카메라가 이동 중에는 분석하지 않도록 하기 위한 방안 문서
---
## Appendix
* VAManager는 사내에서는 Test 할 수 없음.(DB 연동 문제)
* 다수 서버들의 vasvc2 계정으로 실행되는 VAProcess가 일시에 종료되는 증상 있음.
  * Hang check로 인해 재시작 되기는 하나, 같은 시간에 프로세스가 종료되는 현상으로 보아 VAManager에서 죽이는 것으로 보임.

* DNN 서버 한 대가 접속 안되는 상황으로 다음 점검 때 동작 확인이 필요함.

* 20210819_144905_조장연_(guevara23@cudo.co.kr)_[화성시청]_영상분석과_분배시스템간의_소켓_에러메지시_mail.eml
  * 분배 서버에 접속 되지 않아 이벤트 전달이 불가한 현상

* 20220210_151756_조장연_(guevara23@cudo.co.kr)_RE__[화성시청]_접속_ssh_자료_전달mail.eml
  * MPutty Shell 프로그램에서 읽는 화성 시청 서버 접속 정보

