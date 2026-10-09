# korean-prompt-dialogue

한국어로 편하게 말한 아이디어나 수정 요청을 대화로 구체화하고, OpenAI 공식 가이드에 맞는 프롬프트로 작성하는 **Codex 스킬**입니다. 기본 흐름은 **대화 → 프롬프트 제시 → 사용자 승인 → 실행**입니다.

## 어떤 일을 하나요?

- 요청이 명확하면 추가 질문 없이 복사할 프롬프트를 만듭니다.
- 결과가 달라질 만큼 모호한 부분이 있으면, 불편한 장면이나 원하는 변화를 물어봅니다.
- “문구만”, “모바일도”, “일단”, “가능하면” 같은 표현에 담긴 범위와 요청 강도를 보존합니다.
- 대화 중 정정한 내용은 갱신하고, 바꾸지 않은 유지·금지 조건은 남깁니다.
- 다른 AI에 전달할 때도 이해할 수 있도록 필요한 맥락과 자료를 받는 방법을 포함합니다.
- 배경·구체적 지시·결과물 형식·제약·완료 기준을 작성하고, “이 프롬프트로 작업을 진행해도 될까요?”라고 묻습니다.

새 아이디어, 기존 기능 수정, 글쓰기·학습·조사 요청에 사용할 수 있습니다. 스킬을 직접 부르거나 “AI에게 어떻게 요청할지 같이 정리해 줘”처럼 프롬프트 작성 의도가 있는 요청에 적용하며, 일반적인 한국어 질문이나 구현 요청마다 개입하도록 설계하지 않았습니다.

## 설치

Codex에 아래 요청을 그대로 보내세요. `$skill-installer`는 Codex 기본 설치 스킬입니다.

```text
$skill-installer https://github.com/GIY0201/korean-prompt-dialogue/tree/main/skills/korean-prompt-dialogue 에 있는 스킬을 사용자 전역으로 설치해 줘.
```

설치가 끝나면 다음 턴부터 `$korean-prompt-dialogue`로 호출할 수 있습니다. 스킬 자체에는 서버, API 키, 상시 실행 스크립트가 필요하지 않습니다.

## 사용 예

생각을 함께 정리하고 싶을 때:

```text
$korean-prompt-dialogue 검색 기능이 불편한데, 어떻게 바꾸면 좋을지 대화하면서 AI에게 시킬 프롬프트로 정리해 줘.
```

요청이 이미 명확할 때:

```text
$korean-prompt-dialogue 다른 코딩 AI에게 보낼 거야. 회원가입 버튼 문구를 ‘가입’에서 ‘무료로 시작하기’로 바꾸되 디자인과 클릭 동작은 유지하는 프롬프트만 써 줘.
```

이 경우에는 다음처럼 바로 전달할 프롬프트를 만듭니다.

```text
내가 제공하는 프로젝트에서 회원가입 버튼의 문구를 ‘가입’에서 ‘무료로 시작하기’로 바꿔 주세요. 버튼 디자인과 클릭 동작은 유지하세요. 프로젝트에 아직 접근할 수 없다면 관련 파일을 먼저 요청하세요.
```

명확화 후 실행까지 원하면 실행 범위를 함께 지정하세요.

```text
$korean-prompt-dialogue 이 저장소의 README 제목 ‘시작’만 ‘빠른 시작’으로 바꾸는 지시를 정리하고 바로 수정까지 해 줘. 본문은 유지해.
```

프롬프트 작성만 요청하면 작성에서 마칩니다. 일반적인 조사·구현 요청도 기본적으로 완성된 프롬프트를 먼저 보여주고 실행 승인을 기다립니다. 승인 뒤에는 확인한 내용으로 작업하고, 사용자가 수정하면 프롬프트를 갱신해 다시 확인받습니다. 이미 승인한 같은 작업에는 승인을 반복하지 않습니다. “프롬프트 확인은 생략하고 바로 실행해”라고 명시하면 그 범위에서 확인을 생략할 수 있습니다.

작성 기준은 [OpenAI 공식 ChatGPT 프롬프트 가이드](https://developers.openai.com/cookbook/examples/chatgpt/chatgpt_prompt_guide/chatgpt_prompt_guide)를 참고합니다. 적용 방법은 [공식 가이드 적용 규칙](skills/korean-prompt-dialogue/references/openai-prompt-guide.md)에 있습니다.

더 많은 사례는 [대화와 결과 예시](skills/korean-prompt-dialogue/references/examples.md)에서 볼 수 있습니다.

## 저장소 구성

```text
skills/korean-prompt-dialogue/
├── SKILL.md                     # 적용 조건과 대화·작성 규칙
├── agents/openai.yaml           # Codex 표시 및 호출 메타데이터
└── references/
    ├── korean-dialogue.md       # 한국어 의미 해석 참고
    ├── examples.md              # 대화와 결과 예시
    └── openai-prompt-guide.md   # 공식 가이드 적용과 승인 흐름
docs/
├── korean-language-research.md  # 한국어와 대화 연구
├── sources.md                   # 출처와 확인 범위
├── skill-design-plan.md         # 설계와 후속 평가 계획
└── skill-validation.md          # 초기 구현·검증 기록
evals/
├── dialogue-cases.json          # 초기 행동 점검 입력
└── approval-cases.json          # 승인 흐름 수정 후 점검 입력
```

[스킬 본문](skills/korean-prompt-dialogue/SKILL.md)과 [한국어 의미 해석 참고](skills/korean-prompt-dialogue/references/korean-dialogue.md)에 실제 동작 규칙을 담았습니다. 설계 배경은 [한국어와 대화 연구](docs/korean-language-research.md), [출처와 근거](docs/sources.md), [설계 계획](docs/skill-design-plan.md)을 참고하세요.

## 검증 범위

초기 버전의 **12개 대화 사례와 파일 수정 1건** 점검 뒤 실제 사용에서 빠져 있던 프롬프트 승인 단계를 수정했습니다. 수정 후 **5개 대화 사례와 승인 후 파일 수정 1건**으로 승인 대기, 수정 시 재확인, 승인 후 실행과 공식 가이드에 맞는 구성을 점검했습니다. 입력은 [초기 사례](evals/dialogue-cases.json)와 [승인 사례](evals/approval-cases.json), 방법과 한계는 [검증 기록](docs/skill-validation.md)에 있습니다.

이는 소규모 초기 점검입니다. 기본 모델이나 다른 프롬프트 스킬보다 성능이 좋다는 비교 결과는 없으며, 실제 사용자의 장기 대화 부담과 최종 산출물 품질도 아직 평가하지 않았습니다. 다른 도구에서의 호환성은 검증하지 않았습니다.
