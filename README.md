# Insight Generator

## 1. 개요

가치 있는 서비스를 구상하고 수익을 창출하는 것은 많은 도메인 지식과 경험, 통찰이 필요한 영역입니다.
이 영역의 문턱을 자동화된 AI로 낮춰 기존 소수의 사람들만이 구상하던 사업 제안과 구상을 누구나 추상적인 아이디어만으로 웹서비스를 생성합니다.

**Insight Generator**는 사용자의 자연어 요구사항을 입력받아 5단계의 전문 에이전트를 순차적으로 실행하여 완전한 웹 서비스와 문서를 자동 생성하는 **Agentic AI Agent** 시스템입니다.

1. **비즈니스 가치 분석 Agent** - 웹검색을 통해 시장 트렌드를 분석하고, 사내 솔루션조회 MCP Server를 통해 기존솔루션 활용을 고려한 비즈니스 계획 수립
2. **서비스 설계 Agent** - 수립된 비즈니스 계획을 기반으로 구체적인 IT 서비스를 기획
3. **프로젝트 구조분석 Agent** - 기존 코드베이스 구조 분석
4. **코드 생성 Agent** - 실제 동작하는 React 애플리케이션 생성
5. **문서화 Agent** - Docusaurus 기반 종합 문서 생성

---

## 실행방법
```bash
/insight-generator "AI Agent들을 등록/판매하는 솔루션 서비스 생성해줘. https://huggingface.co와 유사하게 만들어주고, 빠르게 시장에 진입해 수익화 할 수 있는 수익모델로 고려해줘"
```

## Agent실행 결과
- React 웹서비스: [http://localhost:5179](http://localhost:5179/)
- 수익화 전략이 포함된 생성 서비스 소개 문서: [http://localhost:4100/docs/category/agenthub](http://localhost:4100/docs/category/agenthub)

## 2. 실제 실행 결과물 캡쳐

### 2.1 AgentHub 애플리케이션

AgentHub는 AI 에이전트를 관리하고 배포하는 플랫폼입니다.

#### 홈페이지
_AgentHub 메인 홈페이지 - AI 에이전트 플랫폼 소개_
![AgentHub Homepage](./images/agenthub-homepage.png)


#### 마켓플레이스
_에이전트 마켓플레이스 - 다양한 AI 에이전트 검색 및 구매_
![AgentHub Marketplace](./images/agenthub-marketplace.png)


#### 워크스페이스
_워크스페이스 - 에이전트 관리 및 모니터링_
![AgentHub Workspace](./images/agenthub-workspace.png)


#### 요금제
_요금제 페이지 - 다양한 구독 플랜 안내_
![AgentHub Pricing](./images/agenthub-pricing.png)

---

### 2.2 Documentation 사이트

문서화 Agent에 의해 생성된 서비스 소개 사이트이며,playWright MCP를 활용해 실행중인 React AgentHub (http://localhost:5179/) 화면을 캡쳐하고 문서화합니다. 

#### AgentHub 개요
_AgentHub 개요 문서 - 플랫폼 소개 및 핵심 기능 설명_
![AgentHub Docs Overview](./images/agenthub-docs-overview.png)


#### 마켓플레이스
_마켓플레이스 문서 - 에이전트 검색, 구매, 판매 가이드_
![AgentHub Docs Marketplace](./images/agenthub-docs-marketplace.png)


#### 워크스페이스
_워크스페이스 문서 - 에이전트 관리 및 설정 방법_
![AgentHub Docs Workspace](./images/agenthub-docs-workspace.png)


#### 크리에이터 스튜디오
_크리에이터 스튜디오 문서 - 에이전트 개발 및 배포 가이드_
![AgentHub Docs Creator Studio](./images/agenthub-docs-creator-studio.png)


#### 요금제
_요금제 문서 - 구독 플랜별 기능 비교_
![AgentHub Docs Pricing](./images/agenthub-docs-pricing.png)


#### 수익 모델 및 수익 창출 방안
_수익 모델 문서 - 크리에이터 수익 창출 전략 및 정산 안내_
![AgentHub Docs Revenue Model](./images/agenthub-docs-revenue-model.png)


## 3. 시스템 아키텍처

### 3.1 전체 파이프라인 흐름

```mermaid
flowchart TB
    subgraph Input["📥 입력"]
        USER[/"사용자 요구사항<br/>$ARGUMENTS"/]
    end

    subgraph Pipeline["🔄 Insight Generator Pipeline"]
        direction TB
        ORCH[["🎯 Pipeline Orchestrator<br/>(insight-generator)"]]

        subgraph Agents["5-Step Agent Pipeline"]
            direction TB
            A1["📊 Step 1<br/>Business Planner"]
            A2["📋 Step 2<br/>Service Planner"]
            A3["🔍 Step 3<br/>Repo Analyzer"]
            A4["⚛️ Step 4<br/>Frontend Generator"]
            A5["📝 Step 5<br/>Doc Generator"]
        end
    end

    subgraph Outputs["📤 출력물"]
        O1[("swarm/trend.json")]
        O2[("swarm/service.json")]
        O3[("swarm/repo-structure.json")]
        O4[("apps/{서비스명}/")]
        O5[("apps/doc/docs/{서비스명}/")]
    end

    USER --> ORCH
    ORCH --> A1
    A1 --> O1
    O1 --> A2
    A2 --> O2
    O2 --> A3
    A3 --> O3
    O3 --> A4
    A4 --> O4
    O4 --> A5
    A5 --> O5

    style ORCH fill:#ff6b6b,stroke:#333,stroke-width:3px,color:#fff
    style A1 fill:#4ecdc4,stroke:#333,stroke-width:2px
    style A2 fill:#45b7d1,stroke:#333,stroke-width:2px
    style A3 fill:#96ceb4,stroke:#333,stroke-width:2px
    style A4 fill:#ffeaa7,stroke:#333,stroke-width:2px
    style A5 fill:#dfe6e9,stroke:#333,stroke-width:2px
```

### 3.2 데이터 흐름 상세

```mermaid
sequenceDiagram
    autonumber
    participant U as 👤 사용자
    participant O as 🎯 Orchestrator
    participant BP as 📊 Business Planner
    participant SP as 📋 Service Planner
    participant RA as 🔍 Repo Analyzer
    participant FG as ⚛️ Frontend Generator
    participant DG as 📝 Doc Generator

    U->>O: 자연어 요구사항 입력

    rect rgb(78, 205, 196)
        Note over O,BP: Step 1: 비즈니스 트렌드 분석
        O->>BP: 요구사항 전달
        BP->>BP: 웹 검색 & 트렌드 분석
        BP-->>O: trend.json 생성
    end

    rect rgb(69, 183, 209)
        Note over O,SP: Step 2: 서비스 기획
        O->>SP: trend.json 전달
        SP->>SP: IT 서비스 설계
        SP-->>O: service.json 생성
    end

    rect rgb(150, 206, 180)
        Note over O,RA: Step 3: 프로젝트 구조 분석
        O->>RA: 프로젝트 분석 요청
        alt repo-structure.json 미존재
            RA->>RA: 폴더/파일 구조 분석
            RA-->>O: repo-structure.json 생성
        else repo-structure.json 존재
            RA-->>O: 건너뛰기
        end
    end

    rect rgb(255, 234, 167)
        Note over O,FG: Step 4: 프론트엔드 생성
        O->>FG: service.json + repo-structure.json 전달
        FG->>FG: React 앱 코드 생성
        FG-->>O: apps/{서비스명}/ 생성
    end

    rect rgb(223, 230, 233)
        Note over O,DG: Step 5: 문서 생성
        O->>DG: 서비스 폴더명 전달
        DG->>DG: 앱 실행 & 스크린샷 캡처
        DG->>DG: Docusaurus MD 파일 생성
        DG-->>O: docs/{서비스명}/ 생성
    end

    O-->>U: ✅ 파이프라인 완료
```

---

## 4. 에이전트 상세 설명

### 4.1 Business Planner (비즈니스 플래너)

| 항목          | 내용                                                    |
| ------------- | ------------------------------------------------------- |
| **역할**      | 시니어 비즈니스 분석가                                  |
| **모델**      | Claude Opus                                             |
| **입력**      | 사용자 자연어 요구사항                                  |
| **출력**      | `swarm/trend.json`                                      |
| **주요 기능** | 웹 검색을 통한 최신 트렌드 분석, 비즈니스 아이디어 도출 |

```mermaid
flowchart LR
    subgraph Input
        REQ["사용자 요구사항"]
    end

    subgraph Process["Business Planner 처리"]
        WS["🌐 웹 검색"]
        TA["📈 트렌드 분석"]
        IA["💡 아이디어 도출"]
    end

    subgraph Output
        JSON["trend.json"]
    end

    REQ --> WS --> TA --> IA --> JSON

    style Process fill:#4ecdc4,stroke:#333
```

### 4.2 Service Planner (서비스 플래너)

| 항목          | 내용                                                 |
| ------------- | ---------------------------------------------------- |
| **역할**      | PM (프로젝트 매니저)                                 |
| **모델**      | Claude Opus                                          |
| **입력**      | `swarm/trend.json`                                   |
| **출력**      | `swarm/service.json`                                 |
| **주요 기능** | 비즈니스 아이디어를 구체적인 IT 서비스 기획으로 변환 |

```mermaid
flowchart LR
    subgraph Input
        TREND["trend.json"]
    end

    subgraph Process["Service Planner 처리"]
        AN["📊 요구사항 분석"]
        DS["🎨 서비스 설계"]
        FD["📄 기능 정의"]
    end

    subgraph Output
        SERVICE["service.json"]
    end

    TREND --> AN --> DS --> FD --> SERVICE

    style Process fill:#45b7d1,stroke:#333
```

### 4.3 Repo Analyzer (저장소 분석기)

| 항목          | 내용                                   |
| ------------- | -------------------------------------- |
| **역할**      | 시니어 React 프론트엔드 개발자         |
| **모델**      | Claude Opus                            |
| **입력**      | 현재 프로젝트 구조                     |
| **출력**      | `swarm/repo-structure.json`            |
| **주요 기능** | 모노레포 구조 분석, 공통 컴포넌트 파악 |

```mermaid
flowchart LR
    subgraph Input
        REPO["프로젝트 구조"]
    end

    subgraph Process["Repo Analyzer 처리"]
        FS["📁 폴더 스캔"]
        PA["🔍 패턴 분석"]
        CC["📦 공통 컴포넌트 식별"]
    end

    subgraph Output
        STRUCT["repo-structure.json"]
    end

    REPO --> FS --> PA --> CC --> STRUCT

    style Process fill:#96ceb4,stroke:#333
```

> **참고**: `repo-structure.json` 파일이 이미 존재하는 경우 이 단계는 건너뜁니다.

### 4.4 Frontend Generator (프론트엔드 생성기)

| 항목          | 내용                                              |
| ------------- | ------------------------------------------------- |
| **역할**      | 시니어 React 웹 프론트엔드 개발자                 |
| **모델**      | Claude Opus                                       |
| **입력**      | `swarm/service.json`, `swarm/repo-structure.json` |
| **출력**      | `apps/{서비스명}/` (React 앱)                     |
| **주요 기능** | 기획서 기반 React 웹 서비스 코드 생성             |

```mermaid
flowchart TB
    subgraph Inputs
        SVC["service.json"]
        REPO["repo-structure.json"]
    end

    subgraph Process["Frontend Generator 처리"]
        direction TB
        SC["🏗️ 스캐폴딩"]
        RC["⚛️ React 컴포넌트 생성"]
        RT["🛤️ 라우팅 설정"]
        ST["🎨 스타일링"]
        CF["⚙️ 설정 파일"]
    end

    subgraph Output
        APP["apps/{서비스명}/<br/>├── src/<br/>├── public/<br/>├── package.json<br/>└── vite.config.ts"]
    end

    SVC --> SC
    REPO --> SC
    SC --> RC --> RT --> ST --> CF --> APP

    style Process fill:#ffeaa7,stroke:#333
```

#### 생성되는 프로젝트 구조

```
apps/{서비스명}/
├── src/
│   ├── components/     # React 컴포넌트
│   ├── pages/          # 페이지 컴포넌트
│   ├── hooks/          # 커스텀 훅
│   ├── utils/          # 유틸리티 함수
│   ├── i18n/           # 다국어 설정
│   ├── App.tsx         # 메인 앱 컴포넌트
│   └── main.tsx        # 진입점
├── public/             # 정적 파일
├── package.json        # 의존성 정의
├── vite.config.ts      # Vite 설정
└── tsconfig.json       # TypeScript 설정
```

### 4.5 Doc Generator (문서 생성기)

| 항목          | 내용                                          |
| ------------- | --------------------------------------------- |
| **역할**      | PM (Docusaurus 문서 작성)                     |
| **모델**      | Claude Opus                                   |
| **입력**      | 생성된 서비스 폴더명, `swarm/service.json`    |
| **출력**      | `apps/doc/docs/{서비스명}/` (Docusaurus 문서) |
| **주요 기능** | 앱 실행, 스크린샷 캡처, MD 문서 생성          |

```mermaid
flowchart TB
    subgraph Input
        SVC_NAME["서비스 폴더명"]
        SVC_JSON["service.json"]
    end

    subgraph Process["Doc Generator 처리"]
        direction TB
        RUN["🚀 앱 실행<br/>pnpm {서비스명}"]
        CFG["📝 스크린샷 설정 생성<br/>screenshot-config.json"]
        CAP["📸 Playwright 스크린샷 캡처"]
        MD["📄 MD 파일 생성"]
        VER["✅ 검증"]
    end

    subgraph Output
        DOCS["apps/doc/docs/{서비스명}/<br/>├── intro.md<br/>├── features.md<br/>├── revenue.md<br/>└── images/<br/>    ├── dashboard.png<br/>    └── ..."]
    end

    SVC_NAME --> RUN
    SVC_JSON --> CFG
    RUN --> CFG --> CAP --> MD --> VER --> DOCS

    style Process fill:#dfe6e9,stroke:#333
```

#### 문서 생성 프로세스

```mermaid
flowchart LR
    subgraph Step1["1단계"]
        A1["앱 실행"]
    end

    subgraph Step2["2단계"]
        A2["설정 파일 생성"]
    end

    subgraph Step3["3단계"]
        A3["스크린샷 캡처"]
    end

    subgraph Step4["4단계"]
        A4["MD 파일 작성"]
    end

    subgraph Step5["5단계"]
        A5["검증 & 테스트"]
    end

    Step1 --> Step2 --> Step3 --> Step4 --> Step5

    style Step1 fill:#e74c3c,color:#fff
    style Step2 fill:#e67e22,color:#fff
    style Step3 fill:#f1c40f,color:#333
    style Step4 fill:#2ecc71,color:#fff
    style Step5 fill:#3498db,color:#fff
```

---

#### Insight Generator 문서

### 5.1 파이프라인 기술

| 구분                | 기술                    |
| ------------------- | ----------------------- |
| **AI 모델**         | Claude Opus (Anthropic) |
| **오케스트레이션**  | Claude Code CLI         |
| **브라우저 자동화** | Playwright              |
| **문서 생성**       | Docusaurus              |

### 5.2 생성되는 프로젝트 기술 스택

```mermaid
flowchart TB
    subgraph Frontend["프론트엔드"]
        REACT["⚛️ React 18"]
        TS["📘 TypeScript"]
        VITE["⚡ Vite"]
        ROUTER["🛤️ React Router"]
    end

    subgraph UI["UI 프레임워크"]
        COMMON["📦 @prime/common-ui"]
    end

    subgraph Build["빌드 & 배포"]
        TURBO["🚀 Turborepo"]
        PNPM["📦 pnpm"]
    end

    subgraph Docs["문서화"]
        DOCU["📚 Docusaurus"]
        MD["📝 Markdown"]
    end

    Frontend --> UI --> Build
    Build --> Docs

    style Frontend fill:#61dafb,stroke:#333
    style UI fill:#764abc,stroke:#333,color:#fff
    style Build fill:#f7df1e,stroke:#333
    style Docs fill:#25c2a0,stroke:#333
```

---

## 6. 모노레포 구조

```mermaid
flowchart TB
    subgraph Root["📁 mono-react-integration"]
        direction TB

        subgraph Apps["apps/"]
            B2B["b2b/"]
            B2C["b2c/"]
            AGENTHUB["agenthub/"]
            DOC["doc/"]
            NEW["✨ {새 서비스}/"]
        end

        subgraph Packages["packages/"]
            COMMON["common-ui/"]
            TSCONFIG["tsconfig/"]
            ESLINT["eslint-config/"]
        end

        subgraph Swarm["swarm/"]
            TREND["trend.json"]
            SERVICE["service.json"]
            REPO_STRUCT["repo-structure.json"]
        end

        subgraph Claude[".claude/"]
            AGENTS["agents/"]
            COMMANDS["commands/"]
        end
    end

    Packages -.->|"공통 컴포넌트 사용"| Apps
    Swarm -.->|"설정 참조"| Apps
    Claude -.->|"에이전트 정의"| Swarm

    style Root fill:#f8f9fa,stroke:#333
    style Apps fill:#e3f2fd,stroke:#333
    style Packages fill:#fff3e0,stroke:#333
    style Swarm fill:#e8f5e9,stroke:#333
    style Claude fill:#fce4ec,stroke:#333
```

---

## 8. 파이프라인 실행 타임라인

```mermaid
gantt
    title Insight Generator 파이프라인 실행 타임라인
    dateFormat HH:mm
    axisFormat %H:%M

    section Step 1
    Business Planner     :a1, 00:00, 5m

    section Step 2
    Service Planner      :a2, after a1, 8m

    section Step 3
    Repo Analyzer        :a3, after a2, 3m

    section Step 4
    Frontend Generator   :a4, after a3, 15m

    section Step 5
    Doc Generator        :a5, after a4, 10m
```

---

_Generated by Insight Generator Pipeline_
_Document Version: 1.0_
_Date: 2025-12-05_
