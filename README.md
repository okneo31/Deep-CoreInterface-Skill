# Software Fundamentals (소프트웨어 펀더멘털)

> **Deep × Core × Interface — 깊음과 핵심 인터페이스**

AI 시대에 좋은 코드를 망치지 않으면서 새 차원을 여는 능력을 위한, 엔지니어링 펀더멘털 + 기획자 형이상학 + 신앙적 근본을 통합한 Claude 스킬.

> "Code is not cheap. Bad code is the most expensive it's ever been." — Matt Pocock
>
> "여호와를 경외하는 것이 지식의 근본이거늘" — 잠언 1:7

이 두 문장이 같은 진술의 두 층위라는 자각 위에서 작동합니다.

🇬🇧 [English version](README.en.md)

---

## 무엇인가

이 저장소는 Matt Pocock의 41만뷰 강연 "Software Fundamentals Matter More Than Ever"의 6가지 함정 회피 원칙과, "decades-old ideas that didn't break, got more important"라고 강조한 4가지 긍정 원칙을 통합한 Claude 스킬 패키지입니다. 거기에 **기획자 형이상학(a~z → -a~z+ → @ → ㄱ~ㅎ)** 과 **"지식의 근본"이라는 신앙적 뿌리**를 통합했습니다.

핵심 명제 한 줄:

> **선한 의도 + 명료함 = 초월**

선한 의도만으로는 흐릿한 결과를 낳고, 명료함만으로는 가짜 초월(다크 패턴)을 낳습니다. 둘 다 갖춰져야 진짜 ㄱ~ㅎ을 만듭니다.

---

## 누구를 위한 것인가

- AI 코딩 시대에 자기 코드베이스의 펀더멘털을 잃지 않으려는 개발자
- "지금 내가 만드는 게 정말 만들어야 할 것인가?"를 매일 묻고 싶은 기획자
- Claude Code에서 모든 코딩 주문 시작 시 자동 발동되는 스킬을 원하는 사람
- 엔지니어링 + 형이상학 + 신앙이 분리되지 않는다고 믿는 사람

---

## 구조

두 가지 형식으로 제공됩니다. 검토 후 선호하는 쪽을 채택하세요.

### V1: Monolith (단일 파일)
```
v1-monolith/
└── SKILL.md
```
한 파일에 모든 원칙 압축. 빠른 발동, 단순 관리.

### V2: Bundle (코어 + 참조)
```
v2-bundle/
├── SKILL.md
└── references/
    ├── PHILOSOPHY.md        — 형이상학 + 신앙적 근본
    ├── SIX_PITFALLS.md      — 회피해야 할 6가지 함정
    ├── CORE_PRACTICES.md    — 지켜야 할 4가지 긍정 원칙
    ├── GRILL_ME_PROTOCOL.md — 의도 추궁 질문 템플릿
    └── DEEP_MODULE_REVIEW.md — Deep/Shallow 판별 체크리스트
```
Progressive disclosure 구조. 각 주제 깊이 있게 분리.

### 영문판
```
en/
├── v1-monolith/SKILL.md
└── v2-bundle/
    ├── SKILL.md
    └── references/ (5개 문서)
```

---

## 핵심 원칙 한 눈에

### 워크플로우 7단계
```
1. Grill Me        의도 추궁
       ↓
2. Spec Lock       명확한 명세
       ↓
3. Module Design   Deep Module + Vertical Slice
       ↓
4. Dependency Check  의존성 3가지 질문
       ↓
5. Build           TDD로 구현
       ↓
6. Review          의식적 코드 리뷰
       ↓
7. Daily Design    매일 시스템 설계에 투자
```

### 6가지 함정 (회피)
① AI가 의도와 다른 걸 만든다 → Grill Me
② 모호한 기획서 → Spec Lock
③ 코드 리뷰의 죽음 → 의식적 리뷰
④ Shallow Module → Deep Module
⑤ 의존성 무지성 추가 → 3가지 질문
⑥ 설계 부재 → 매일의 설계

### 4가지 긍정 원칙 (실천)
① Ubiquitous Language — 비즈니스/코드/UI 언어 통일 (Eric Evans)
② Vertical Slices — 끝에서 끝까지 한 슬라이스 (XP/Agile)
③ TDD — 테스트가 명세 (Kent Beck)
④ Deep Modules — 단순 인터페이스 + 풍부한 내부 (John Ousterhout)

---

## 사용법

### Claude Code에서 (가장 권장)

```bash
# V2 번들 권장
cp -r v2-bundle ~/.claude/skills/software-fundamentals/

# 또는 V1 단일 파일
mkdir -p ~/.claude/skills/software-fundamentals
cp v1-monolith/SKILL.md ~/.claude/skills/software-fundamentals/
```

이후 새 코딩 주문 시작 시 Claude Code가 자동으로 SKILL.md의 description에 명시된 트리거 키워드를 감지하여 워크플로우를 따릅니다.

### Claude.ai에서

프로젝트 시스템 프롬프트 또는 메모리에 SKILL.md 내용을 통합하거나, 새 대화 시작 시 "이 스킬을 따라주세요"라며 첨부하시면 됩니다.

### 일반 참고용으로

이 저장소 자체가 좋은 코드 작성 원칙에 대한 한 권의 작은 책이 될 수 있습니다. PHILOSOPHY.md → SIX_PITFALLS.md → CORE_PRACTICES.md → GRILL_ME_PROTOCOL.md → DEEP_MODULE_REVIEW.md 순으로 읽기 권장.

---

## 출처

### 영상
- **원본 강연 (영어):** Matt Pocock, "Software Fundamentals Matter More Than Ever" (2026.4.23 초연) — https://youtu.be/v4F1gFy-hqg
- **한국어 해설판:** AgentOS 채널 — https://youtu.be/FOee3zb98wI

### 책 / 사람
- Eric Evans, *Domain-Driven Design* (Ubiquitous Language)
- Kent Beck, *Test-Driven Development: By Example*, *Tidy First?*
- John Ousterhout, *A Philosophy of Software Design* (Deep Modules)
- XP(Extreme Programming) / Agile 운동 (Vertical Slices)
- Matt Pocock GitHub Skills: https://github.com/mattpocock/skills

### 성경
잠언 1:7, 18:13, 20:5, 22:3, 25:2 / 창세기 1:1, 1:31, 11:6 / 마태복음 21:19 / 누가복음 7:7-8, 14:28-30 / 빌립보서 3:13-14 / 데살로니가전서 5:21 / 야고보서 1:22

---

## 한 줄 요약

> 📖 **창세기 1:31** — "하나님이 지으신 그 모든 것을 보시니 보시기에 심히 좋았더라"
>
> 이 한 마디가 모든 작업의 끝에서 들리도록 하라. 그러면 그 작업은 ㄱ~ㅎ을 만든 것이다.

---

## 라이선스

MIT License (제안). 자유롭게 사용·수정·재배포 가능. 원본 출처(Matt Pocock의 원본 강연)에 대한 credit을 유지해 주세요.

---

## 저자

**Neo (안재현)** · TTL Inc. (주식회사 티티엘)

- Matt Pocock의 강연 원칙을 한국어로 정리·확장
- 기획자 형이상학(a~z → ㄱ~ㅎ)과 신앙적 근본(잠언 1:7 / 창세기 1:31) 통합
- 15개 TTL 프로젝트 사례 적용

---

## 기여

PR 환영. 다음 영역에서 특히 의견 받습니다:
- 추가 어울리는 성경 구절 후보
- 다른 언어/문화권의 동등한 형이상학 비유
- TTL 외 프로젝트 사례 (한국어 사용자가 기여하는 자기 사례)
- 영문 번역 다듬기

이슈도 자유롭게 열어주세요.
