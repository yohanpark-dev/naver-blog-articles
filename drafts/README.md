# drafts/

작성 중인 글이 머무는 곳입니다.

새 글은 항상 이 폴더에서 시작합니다. `templates/post-template.md`를 복사해서 만들거나, Claude Code에서 `/new-post` 명령으로 자동 생성합니다.

파일명 형식은 `YYYY-MM-DD-slug.md`이며, 여기서 `YYYY-MM-DD`는 작성 시작일(`date_created`)입니다. 발행 시점에 파일명을 발행일로 바꾸지 않아도 됩니다. frontmatter의 `date_published`가 발행일을 별도로 추적합니다.

발행이 완료되면 이 폴더의 파일을 `posts/`로 옮깁니다. `git mv` 명령으로 옮기면 이력이 보존되어 나중에 글의 변화 과정을 추적할 수 있습니다.
