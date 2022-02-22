# KT VA

## Git Server
* VA Process
  * http://172.16.4.99/administrator/VAProcess_VS.git
  * Branch : VAProcess_KT

* VA Manager
  * http://172.16.4.99/administrator/VAManager.git
  * Branch : VAManager_kt

---

## 문서 설명
* application properties
  * KT VAManager 설정 파일. 각 값에 주석 참고

* KT Manager 동작 시나리오.pptx
  * Manager의 동작 시나리오
  * 운용자 메뉴얼, 인터페이스 정의서 참고

* KT 설치 방법.docx

* VSaaS 2018 3rd Party 인터페이스 정의서(VA)-v3.07-Rev5
  * 2019.10.28 기준 연동 인터페이스
  * KT Rest 연동 규격 문서 최신버전
  * 단, 일부 맞지 않는 규격이 있을 수 있음.(메일 참고)

* VSAAS플랫폼_운용자매뉴얼_IVX_VA_20191203
  * From. 오범석 수석
  * 동작 시나리오 설명

* 로드밴런스 공식.jpg
  * 영상 분석 요청이 있거나, 절체시 위 그림의 공식으로 계산되어서 서버에 할당 됨.
  * **해당 내용 필요**

---

## 문서 외 시나리오
* 영상 분석 요청 메시지
  * VA_10001, VA_10003 두개의 영상 분석 요청 메시지가 있으며 10001은 한 개 요청, 10003은 여러 개 요청으로 설계됨.
  * 실 서버에서는 KT 측에서 10003으로 영상 요청이 들어옴.
  * 10001은 스냅샷 문제로 직접 요청하지 않고, VAManager 내부에서 10003 요청이 올 경우, 함수에서 10001 사용
  * VixOne #1618 확인

---

## KT Test Server 정보
* TB 서버
* 121.135.203.216 ~ 121.135.203.218
* ID : gigasurv
* PW : dudjdTkd34%^ (여영쌍34%^)

---

## 기타 전달 내용
* 2019년 5월 까지 작업 내용은 프리랜서가 작업함. 작업당시 이력 관리가 되지 않았음
* 사내에서 테스트 불가능. 개발 당시, KT 개발망에서 직접개발함. 