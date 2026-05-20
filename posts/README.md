# posts/

발행이 완료된 글이 모이는 곳입니다.

파일명 형식은 `YYYY-MM-DD-slug.md`이며, `YYYY-MM-DD`는 발행일이고 `slug`는 frontmatter의 slug와 일치합니다. 예: `2026-05-19-ms365-copilot-first-month.md`.

발행 후에도 frontmatter는 그대로 유지됩니다. `status: published`, `date_published`, `naver_url` 항목이 채워져 있어야 합니다.

`drafts/`에서 옮겨질 때는 일반적으로 git으로 `git mv` 명령을 써서 이력을 보존합니다. 이 폴더에 직접 새 파일을 만들지 않습니다. 모든 글은 `drafts/`에서 시작합니다.
