# /find-related — 이전 글 매칭

사용자가 작성 중인 글과 관련된 이전 글을 찾으려고 합니다. 매칭은 자동화되지 않고, 후보를 사람에게 제시하고 사람이 결정합니다.

## 1. 대상 글 확인

현재 사용자가 어느 글을 다루고 있는지 확인합니다. 인자로 파일 경로가 주어졌다면 그 파일을, 아니라면 가장 최근에 수정된 `drafts/` 안의 파일을 대상으로 합니다.

대상 글의 frontmatter에서 `topic_keywords`, `tags`, `category`를 읽습니다.

## 2. 후보 수집

`posts/`와 `drafts/` 안의 모든 마크다운 파일을 훑어 각 파일의 frontmatter를 읽고, 다음 기준으로 점수를 매깁니다.

- `topic_keywords`가 하나라도 겹치면 강한 후보 (높은 점수)
- `tags`만 겹치면 중간 후보
- `category`만 같으면 약한 후보

대상 글 자신은 후보에서 제외합니다.

## 3. 후보 보고

후보를 점수 높은 순으로 정렬해서 사용자에게 보고합니다. 각 후보에 대해 다음을 표시합니다.

- 파일명과 글 제목
- 겹치는 키워드/태그가 무엇인지
- `date_published` 또는 `date_created`
- `status` (published / draft / archived)

후보가 5개를 넘으면 상위 5개만 보여주고, 나머지는 "그 외 N개의 약한 후보가 더 있습니다. 보시겠습니까?"라고 안내합니다.

## 4. 선택과 적용

사용자가 어떤 후보를 `related_posts`에 추가할지 선택하면, 대상 글의 frontmatter `related_posts` 배열에 추가합니다. 이미 들어 있는 항목은 중복으로 추가하지 않습니다.

## 5. 양방향 연결 검토

`related_posts`에 추가한 글이 발행 완료된 글(posts/ 폴더에 있고 status가 published)이라면, "그 글의 frontmatter에 이번 글을 supersedes나 related로 연결할까요?"라고 묻습니다.

- 이번 글이 이전 글의 내용을 갱신하는 경우: 이번 글의 `supersedes`에 이전 글 slug, 이전 글의 `superseded_by`에 이번 글 slug를 적습니다.
- 갱신이 아니라 단순 관련: 이전 글의 `related_posts`에도 이번 글 slug를 추가합니다.

이 작업은 발행된 글의 frontmatter를 수정하는 행위이므로, 적용 전 사용자 확인을 한 번 더 받습니다.
