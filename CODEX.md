# Codex 작업 참고

이 저장소는 yohanpark.dev의 네이버 블로그 글 초안을 GitHub에서 관리하는 문서 저장소입니다. GitHub의 Markdown 파일이 단일 진실의 원천이고, 네이버 블로그 글은 사람이 직접 옮긴 결과물입니다. 정정과 갱신은 항상 GitHub를 먼저 고친 뒤 네이버 블로그에 반영합니다.

## 최우선 원칙

- 본문 문장은 AI가 작성하지 않습니다. Codex는 구조 제안, 자료 조사, frontmatter 정리, 발행 전 검사, 정정 절차 보조, 관련 글 후보 제시까지만 담당합니다.
- 사용자가 `<pre></pre>` 태그로 감싼 내용은 사람이 직접 작성한 영역입니다. 읽고 확인할 수는 있지만 문장을 고치거나 다시 쓰지 않습니다.
- 출처 정책은 `references/README.md`를 최우선 기준으로 따릅니다. 다른 문서의 요약과 충돌하면 `references/README.md`가 우선합니다.
- `references/README.md`는 사용자가 직접 관리하는 파일입니다. 사용자의 명시적 요청이 없으면 Codex는 이 파일을 수정하거나 항목을 추가하지 않고 읽기만 합니다.
- 구체적인 출처 이름, 도메인, URL은 `references/README.md`에만 둡니다. 이 문서를 포함한 다른 문서에는 직접적인 출처 이름이나 URL을 적지 않고 `references/README.md`를 가리키기만 합니다. (글 frontmatter의 `sources`에 적는 실제 인용 자료의 제목·URL은 예외입니다.)
- 인용할 때는 URL만 적지 않고, 원문 문장을 frontmatter의 `sources.<type>[].quotes[].text`에 그대로 기록합니다. 한 인용 문장은 200자 이내로 유지합니다.

## 프로젝트 구조

- `README.md`: 저장소 개요와 큰 운영 원칙.
- `CODEX.md`: Codex가 작업 시작 시 빠르게 읽을 요약 지침.
- `.claude/CLAUDE.md`: Claude Code용 핵심 지침. Codex 작업도 이 원칙을 따라야 합니다.
- `.claude/commands/`: `/new-post`, `/find-related`, `/publish-check`, `/add-correction`, `/plan-week` 동작 정의.
- `docs/`: 자세한 운영 문서.
  - `docs/writing-guide.md`: 글쓰기 원칙, 톤, 인용, 정정 철학.
  - `docs/frontmatter-schema.md`: frontmatter 필드 의미와 형식.
  - `docs/workflow.md`: 새 글 시작부터 발행, 정정, 후속 글까지의 흐름.
- `templates/`: 새 글의 시작 템플릿 모음. `post-template.md`(일반 글), `qna-template.md`(대화형 Q&A 글).
- `drafts/`: 작성 중인 글. 모든 새 글은 여기서 시작합니다.
- `posts/`: 발행 완료 글. `drafts/`에서 발행 후 이동합니다.
- `references/`: 허용 출처 기준. `references/README.md`가 출처 정책의 최우선 원본입니다.
- `scripts/`: 반복 작업이 충분히 쌓였을 때 자동화 스크립트를 둘 자리. 현재는 비어 있어도 정상입니다.

## 출처 정책

출처 정책의 최우선 기준은 `references/README.md`입니다. 허용 출처와 사용하지 않는 출처의 구체적인 이름·도메인은 모두 그 파일에 있습니다. Codex는 출처를 다룰 때마다 `references/README.md`를 읽어 기준을 확인하고, 이 문서를 포함한 다른 문서에는 직접적인 출처 이름이나 URL을 적지 않습니다.

자료 조사 중 허용 기준 밖의 자료를 참고할 수는 있어도, 글 frontmatter의 `sources`에는 `references/README.md`의 허용 출처만 기록합니다.

## 글 파일 규칙

- 파일명은 `YYYY-MM-DD-slug.md` 형식입니다.
- `drafts/`의 날짜는 작성 시작일입니다.
- `posts/`의 날짜는 발행일이며, `date_published`와 맞아야 합니다.
- `slug`는 영문 소문자와 하이픈만 사용합니다.
- 새 글은 `templates/`의 템플릿(`post-template.md` 또는 `qna-template.md`)을 복사해 `drafts/`에서 시작합니다. 별도 지정이 없으면 `post-template.md`를 씁니다.
- 발행 후 이동은 가능하면 `git mv`로 처리해 이력을 보존합니다.

## Frontmatter 핵심 필드

발행 전 최소한 다음 항목이 채워져 있어야 합니다.

- 식별: `title`, `slug`, `date_created`, `category`, `tags`, `topic_keywords`, `volatility`
- AI 사용 기록: `ai_usage.short_summary`, `ai_usage.tools_used`, `ai_usage.used_for`, `ai_usage.not_used_for`
- 검증 환경: `test_environment.plan`, `test_environment.period`, `test_environment.os`, `test_environment.apps_tested`
- 출처: 사용한 자료마다 `title`, `url`, `quotes.text`, `quotes.cited_in`

`related_posts`는 자동으로 추가하지 않습니다. Codex는 후보만 제시하고, 사용자가 선택한 항목만 반영합니다.

## 작업별 기준

### 새 글 시작

사용자에게 제목, slug, category, topic_keywords, volatility, 검증 환경을 확인합니다. 이후 `posts/`와 `drafts/`의 기존 글을 훑어 관련 후보를 제시합니다. 사용자가 고른 관련 글만 `related_posts`에 넣습니다. 본문은 템플릿 그대로 두고 작성하지 않습니다.

### 자료 조사

공식 자료를 찾고 핵심 내용을 정리할 수 있습니다. 단, 최종 출처 후보는 `references/README.md`의 허용 기준에 맞는지 확인합니다. frontmatter에 넣을 때는 인용할 원문 문장과 `cited_in` 자리까지 함께 준비합니다.

### 발행 전 검사

`/publish-check` 기준을 따릅니다. 문제를 발견하면 위치와 이유를 보고합니다. 사용자 확인 없이 본문이나 frontmatter를 자동 수정하지 않습니다.

### 정정

정정은 `factual`과 `minor`로 나눕니다. 판단이 애매하면 `factual`로 처리합니다. 원본 본문은 지우지 않고, frontmatter `corrections`, 본문 상단 정정 안내, 본문 내 정정 표시, 하단 `정정 이력`을 서로 일치시킵니다. `factual`은 GitHub Issue 링크가 필요합니다.

## 톤과 형식

- 본문은 `~다`체 또는 `~습니다`체 중 하나로 통일합니다.
- 권장 본문 길이는 frontmatter 제외 3500~4500자입니다.
- 시스템 기호 외 이모지는 쓰지 않습니다.
- AI 클리셰 표현은 피합니다. 예: `~에 대해 알아보겠습니다`, `결론적으로`, `오늘은 ~에 대해`, `한 번 살펴보겠습니다`, `여러분`, `이번 시간에는`, `함께 알아보아요`.

## 먼저 읽을 문서

작업 성격별로 다음 문서를 우선 확인합니다.

- 구조 파악: `README.md`, 이 파일
- 글쓰기/톤 판단: `docs/writing-guide.md`
- frontmatter 편집: `docs/frontmatter-schema.md`
- 발행/정정 흐름: `docs/workflow.md`
- 명령 동작 재현: `.claude/commands/*.md`
