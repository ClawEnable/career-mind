[English](../README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | **[한국어](README.ko.md)**

# career-mind

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE) [![Version](https://img.shields.io/badge/version-0.7.0-green.svg)](../.claude-plugin/marketplace.json)

AI 코딩 에이전트를 위한 커리어 역량 관리 도구. 모든 소스에서 역량 정보를 수집하고, 정보 품질을 평가하며, 모든 시나리오에 맞는 커리어 산출물을 생성——이력서, 성과 리뷰, 승진 사례 등.

**조작된 성과 없음. 모든 출력은 실제 경험으로 추적 가능합니다.**

## 빠른 시작

```bash
git clone https://github.com/ClawEnable/career-mind.git
cp -r career-mind/skills/* ~/.claude/skills/   # 또는 에이전트의 스킬 경로
```

에이전트에서 `/career-mind:cm-init`을 실행하여 시작하세요.

## 지원 에이전트

| 에이전트 | 스킬 경로 | 설치 방법 |
|---------|----------|----------|
| Claude Code | `~/.claude/skills/` | 플러그인 마켓플레이스 또는 수동 복사 |
| Codex | `~/.agents/skills/` | `$skill-installer` 또는 수동 복사 |
| Cursor | `~/.agents/skills/` 또는 `~/.cursor/skills/` | GitHub 원격 가져오기 또는 수동 복사 |
| OpenCode | `.opencode/skills/` | 수동 복사 |
| OpenClaw | `<workspace>/skills/` | `openclaw skills install` |

## 설치

### Claude Code

플러그인 마켓플레이스 (권장):

```
/plugin marketplace add ClawEnable/career-mind
/plugin install career-mind@career-mind
```

또는 수동 설치:

```bash
git clone https://github.com/ClawEnable/career-mind.git
cp -r career-mind/skills/* ~/.claude/skills/
```

### OpenClaw

```bash
openclaw skills install career-mind
```

### 기타 에이전트

`skills/` 디렉토리를 에이전트의 스킬 경로에 복사 (위 표 참조):

```bash
git clone https://github.com/ClawEnable/career-mind.git
cp -r career-mind/skills/* ~/.agents/skills/   # Codex, Cursor, OpenCode
```

## 스킬 목록

| 명령 | 설명 |
|------|------|
| `/career-mind:cm-init` | 커리어 컨텍스트 초기화——문서 스캔, 프로필 수집, 기존 자료 가져오기 |
| `/career-mind:cm-capture` | 도메인 인식 옵션 기반 상호작용으로 역량 수집: 가져오기 후 분석, 능동적 설명, 세션 리뷰, 문서 가져오기 |
| `/career-mind:cm-assess` | 정보 품질을 평가하고 진단 인사이트와 실행 가능한 권장 사항 제공 |
| `/career-mind:cm-craft` | 커리어 산출물 생성: 이력서, 성과 리뷰, 승진 사례, 스킬 맵 |
| `/career-mind:cm-interview` | 면접 준비: 기술, 행동, 협업 질문 및 구조화된 모의 면접 |
| `/career-mind:cm-status` | 현재 상태 확인 및 다음 단계 권장 |

## 작동 방식

플러그인은 경험 많은 전문가를 위해 설계된 도메인 우선 상호작용 모델을 사용:

- **도메인 추론**——질문하기 전에 기술 콘텐츠를 먼저 이해하므로 일반적인 관행에 대한 설명을 요구하지 않음
- **옵션 기반 수집**——추정값이 포함된 세련된 서술 옵션을 생성하여 처음부터 작성하는 대신 확인 또는 수정
- **자문 권장**——선택지를 제시하기만 하는 것이 아니라 이유와 함께 권장
- **커리어 단계 적응**——커리어 단계에 따라 전략 조정: 신입, 미드 커리어, 시니어, 전직
- **동적 관점**——분석이 대상 역할에 맞게 조정; 아키텍트에게 중요한 갭이 시니어 엔지니어에게는 사소할 수 있음
- **반복적 정제**——각 선택이 새로운 단서를 드러내며 구조화된 라운드를 통해 정확한 서술로 수렴

```
cm-init → cm-capture ⇄ cm-assess → cm-craft (모든 시나리오) → cm-interview (선택)
                   ↑              │
                   └──────────────┘  (cm-assess가 갭 발견 → cm-capture로 보완)
```

필요에 따라 어디서든 시작:

- 아무것도 없음 → `/career-mind:cm-init`
- 경험을 기술하고 싶음 → `/career-mind:cm-capture`
- 기존 내용을 평가하고 싶음 → `/career-mind:cm-assess`
- 특정 산출물이 필요 → `/career-mind:cm-craft`
- 면접 준비 → `/career-mind:cm-interview`
- 잘 모르겠음 → `/career-mind:cm-status`

## 데이터 저장

모든 데이터는 현재 작업 디렉토리의 `.career/`에 저장:

```
.career/
├── profile.md       # 이름, 연락처, 학력 (지속적으로 보완 가능)
├── context.md       # 스킬 간 상태 (YAML frontmatter)
├── entries/         # 역량 라이브러리 (project, signal, achievement 항목)
└── outputs/         # 생성된 산출물 (이력서, 평가 보고서 등)
```

## 개인정보

**모든 개인 데이터는 프로젝트 디렉토리의 `.career/`에 저장됩니다.** 프로필, 항목 및 생성된 산출물은 명시적으로 공유하지 않는 한 로컬 머신을 떠나지 않습니다. Git 추적을 원하지 않으면 `.career/`를 `.gitignore`에 추가하세요.

## 조작 방지

플러그인은 엄격한 소스 추적을 적용:

- `/career-mind:cm-craft`에서 생성된 각 산출물 항목은 검증된 소스로 추적 가능 (별도의 `.meta.md` 파일에 기록)
- 소스는 다음으로 제한: 항목 라이브러리, 프로필 데이터, 또는 사용자의 직접적인 말
- 조작된 지표, 과장된 스킬, 허위 성과 없음
- 한정적 맥락은 성과와 함께 보존——증거를 선택적으로 제시하여 인식되는 범위를 부풀리지 않음

## 기여

스킬, 평가 차원, 출력 시나리오 추가에 대한 지침은 [CONTRIBUTING.md](../CONTRIBUTING.md)를 참조하세요.

## 라이선스

[MIT](../LICENSE) © 2026 ClawEnable
