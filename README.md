# 🛠️ Workspace Setup

백엔드 개발자를 위한 효율적인 로컬 디렉토리 구조 및 환경 설정 가이드
데이터의 **중요도(Value)**와 **수명(Lifecycle)**에 따라 백업 영역(`Dev`)과 비백업 영역을 철저히 분리하여 생산성과 유지보수성을 극대화할 수 있도록 시도했습니다.

## 🎯 전재조건

1. **Backup Strategy:** `Dev` 폴더만 동기화(Cloud/HDD)하면 모든 업무 환경이 보존되어야 합니다.
3.  **Fast Recovery:** OS 재설치 시 `config`와 `tools`만으로 거의 모든 환경이 복구 가능해야 합니다.

<br>

## 📂 Directory Structure

```text
UserHome(ex: Z드라이브 루트)/
├── Dev/                     # [Sync] Cloud Drive (Dropbox, OneDrive, etc.) 혹은 주기적으로 외장하드 백업
│  ├── work/                 # 회사 업무 (Git 계정 분리 필수)
│  ├── projects/             # 개인/팀 포트폴리오 (GitHub 관리)
│  ├── study/                # 학습 코드, 알고리즘 풀이
│  ├── config/               # IDE 설정, Dotfiles (.zshrc, .gitconfig)
│  ├── scripts/              # 자동화 쉘 스크립트, 개인 CLI 도구
│  ├── tools/                # 설치가 필요 없는 Portable 프로그램
│  ├── resources/            # 공용 테스트 데이터, 아이콘, 폰트
│  ├── documents/            # 기술 문서, 기획서
│  └── archive/              # 종료된 프로젝트 (Zip 압축 보관)
│
└── /                        # [No-Sync]
   ├── Temp/                 # 임시 파일 (주기적 삭제)
   ├── Cache/                # 빌드 아티팩트 (.m2, .gradle, npm_modules)
   ├── SDKs/                 # JDK, Android SDK, Node binaries
   └── VMs/                  # 가상머신 이미지 (.vdi, .iso)

```

## 📝 Detailed Description

### 1. Dev (백업 필수 영역)

| 폴더명 | 설명 및 용도 |
| --- | --- |
| **work** | 회사 소스코드. 개인 포트폴리오와 분리하여 관리. |
| **projects** | 개인(`personal`) 및 팀(`team`) 프로젝트. GitHub 연동 필수. |
| **study** | 강의 실습, 토이 코드, 알고리즘 문제 풀이 등 학습 기록. |
| **config** | 개발 환경 설정 백업. (IntelliJ Settings, VS Code JSON, Terminals) |
| **scripts** | 반복 작업을 자동화하는 스크립트 모음. (PATH 등록 권장) |
| **tools** | 설치 없이 실행 가능한 포터블 유틸리티 (Putty, DBeaver 등). |
| **resources** | 프로젝트 간 공유되는 더미 데이터(JSON/CSV), 디자인 에셋. |
| **archive** | 더 이상 유지보수하지 않는 종료된 프로젝트 저장소. |

### 2. Local (백업 제외 영역)

> **핵심:** 언제든 인터넷에서 다시 구할 수 있거나, 빌드하면 생성되는 것.

| 폴더명 | 설명 및 용도 |
| --- | --- |
| **Temp** | 다운로드 파일, 1회성 테스트 코드, 압축 해제용 공간. |
| **Cache** | 패키지 매니저 캐시(`.m2`, `.gradle`), Docker Volumes. |
| **SDKs** | JDK, Android SDK 등 대용량 바이너리. |
| **VMs** | VirtualBox, VMWare 등 대용량 가상 OS 이미지. |


### 2. 환경 변수 등록 (PATH)

`tools`와 `scripts` 폴더를 시스템 경로에 추가하여 어디서든 실행 가능하게 합니다.

```bash
# .zshrc or .bash_profile
export DEV_HOME="$HOME/Dev"
export PATH="$PATH:$DEV_HOME/scripts:$DEV_HOME/tools"

```
