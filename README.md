# 웨딩 에디터 프로젝트

이 프로젝트는 웨딩 에디터 애플리케이션입니다.

## 컴포넌트 구조

컴포넌트는 다음 디렉토리로 구성됩니다:

- `src/components/blocks`: 개별 블록 컴포넌트(예: `AccountBlock.vue`, `ContactBlock.vue`)를 포함합니다. 이들은 편집 가능한 콘텐츠 블록입니다.
- `src/components/previews`: 각 블록에 대한 미리보기 컴포넌트(예: `AccountPreview.vue`, `ContactPreview.vue`)를 포함합니다. 이들은 최종 결과물에서 블록이 어떻게 보일지 표시합니다.
- `src/components/common`: 애플리케이션 전반에 사용되는 공통 및 유틸리티 컴포넌트(예: `BlockSelector.vue`, `Editor.vue`, `Preview.vue`)를 포함합니다.
