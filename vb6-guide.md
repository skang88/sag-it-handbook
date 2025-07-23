# Visual Basic 6.0 개발환경 셋팅 및 ERP 업데이트 배포 가이드

## 1. Visual Basic 6.0 개발환경 셋팅

1. Visual Basic 개발 환경 셋팅 파일 해제  
   - 위치: 내부 파일서버(예: \\[내부경로]\Software\VisualBasic\)
2. Visual Basic 6.0 Enterprise 설치  
   - ISO 파일을 더블클릭하여 CD1 이미지를 삽입  
   - 설치 시 제품번호는 예시값 사용(공개 배포 불가, 내부 참고)  
   - 사용자 정의 설치에서 필요 없는 컴포넌트(예: SourceSafe, ActiveX 등)는 체크 해제  
   - 설치가 정상적으로 완료되지 않으면 재설치 시도
3. 재부팅 후 MSDN 설치 안내는 무시(이미지 디스크 마운트가 안될 경우 무시)
4. 설치 경로 예시: `C:\Program Files (x86)\Microsoft Visual Studio\VB98\VB6.exe`  
   - 관리자 권한으로 실행 후 정상 동작 확인

### VB 모듈 및 관련 컴포넌트 설치

- 각종 OCX, DLL, 런타임 등은 내부 배포 폴더에서 관리자 권한으로 설치
- 예시: `setup_64bit`, `Visual Basic 6 Runtimes Pack`, `Crystal Report`, `Spread`, `Chartfx`, `Unitesuite` 등
- OCX 등록: `regsvr32` 명령어 사용

---

## 2. Visual Basic 6.0 ERP 업데이트 및 배포 방법

### 소스코드 및 프로그램 관리

- 소스코드는 내부 파일서버(예: \\[내부경로]\SAG\Project\)에서 관리
- 컴파일된 프로그램 파일은 별도 폴더에 저장

### 서버에 프로그램 배포 및 버전 관리

- 서버의 지정된 폴더(예: D:\[내부경로]\CS_Program\SAG)에 컴파일된 파일을 복사
- 파일 버전 및 업데이트 내역은 별도 관리 테이블(예: FILE_UPDATE)에서 날짜/시간으로 관리
- 업데이트된 파일을 각 PC에서 내려받아 최신 소프트웨어로 설치

---

> ※ 본 문서의 경로, 서버명, IP 등은 모두 예시로 표기하였으며, 실제 정보는 내부 정책에 따라 별도 관리 바랍니다.
