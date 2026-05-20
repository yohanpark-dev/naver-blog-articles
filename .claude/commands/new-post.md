# /new-post — 새 글 시작

사용자가 새 블로그 글을 시작하려고 합니다. 다음 절차를 따릅니다.

## 1. 사용자에게 묻기

다음 정보를 한 번에 모아 묻습니다.

- 글 제목 (한국어, 네이버 블로그에 그대로 들어갈 형태)
- 글 식별자(slug, 영문 소문자 + 하이픈, 예: ms365-copilot-first-month)
- 글의 큰 분류(category, 예: tech-review, work-tool, education)
- 핵심 주제 키워드(topic_keywords) 2~4개. 이전 글과 매칭에 쓰입니다. 너무 추상적이지 않게, 구체적인 주제로 적도록 안내합니다(예: "copilot" 대신 "copilot-korean-quality", "copilot-licensing").
- 글의 수명(volatility): high(빠르게 낡음) / medium(보통) / low(잘 안 낡음). 짧은 설명과 함께 묻습니다.
- 검증 환경: 사용 플랜, 검증 시점, OS, 주로 검증한 앱.

## 2. 이전 글 매칭 (반자동)

위 정보를 받은 직후, `posts/`와 `drafts/` 폴더의 모든 마크다운 파일을 훑어서 frontmatter의 `topic_keywords`가 사용자가 답한 키워드와 겹치는 글을 후보로 제시합니다. 후보가 있으면 다음과 같이 보고합니다.

> 다음 글들이 비슷한 주제를 다룹니다. 관련 글로 연결할 항목을 선택해 주세요.
> 1. 2026-01-15-copilot-first-impression — "Copilot 첫인상" (겹치는 키워드: copilot-korean-quality)
> 2. 2026-03-08-ms365-licensing — "MS365 라이선스 비교" (겹치는 키워드: copilot-licensing)

사용자가 선택한 것만 `related_posts`에 추가합니다. **자동으로 추가하지 않습니다.** 매칭 결정은 항상 사람의 몫입니다.

후보가 없으면 "겹치는 주제의 이전 글은 없습니다"라고 보고합니다.

## 3. 파일 생성

`templates/post-template.md`를 `drafts/YYYY-MM-DD-slug.md`로 복사합니다. `YYYY-MM-DD`는 오늘 날짜, `slug`는 사용자가 답한 값입니다.

복사한 파일의 frontmatter에서 다음 항목을 채웁니다.

- `title`, `slug`, `date_created` (오늘)
- `category`, `tags` (사용자가 답한 분류 + 관련 키워드)
- `topic_keywords`
- `volatility`
- `related_posts` (2단계에서 사용자가 선택한 것)
- `test_environment` 하위 항목들

본문(frontmatter 아래의 모든 내용)은 손대지 않습니다. 템플릿의 가이드 문구가 그대로 남아 있어야 사용자가 그 위에 본문을 채울 수 있습니다.

`ai_usage`와 `sources` 항목은 비워둡니다. 글 작성이 진행되면서 채워집니다.

## 4. Linear 이슈 생성

`/plan-week`로 일정을 잡을 때 이미 만들어진 Linear 이슈가 있다면 그 ID를 frontmatter `linear_issue_id`에 적습니다.

이슈가 없다면 사용자에게 "Linear에 이슈를 만들고 ID를 frontmatter에 연결할까요?"라고 묻습니다. 사용자가 예라고 하면 Linear MCP를 사용해 `yohanpark-dev-docs` 팀의 "네이버 블로그 글" 프로젝트에 이슈를 생성하고 ID(`YDOC-1` 형식)를 적습니다.

## 5. 자료 조사 안내

파일을 만든 후, 사용자에게 다음과 같이 안내합니다.

> 새 글 파일이 만들어졌습니다.
>
> 다음으로 자료 조사를 진행하시면 됩니다. 자료를 찾을 때마다 frontmatter의 `sources`에 즉시 추가하는 것이 좋습니다. 이때 URL뿐 아니라 **인용할 원문 문장**(`quotes.text`)을 함께 적어두세요. 본문에서 그 문장을 어느 절에서 인용할지는 본문을 쓰면서 결정해도 됩니다.
>
> 본문 작성은 사용자께서 직접 하시는 영역입니다. 자료 조사나 구조 점검이 필요하시면 말씀해 주세요.

본문 작성을 자청하지 않습니다.
