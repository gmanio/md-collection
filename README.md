# md-collection

Markdown 파일을 저장/관리하고 GitHub Pages로 렌더링하기 위한 저장소입니다.

## 구성

- `index.md`: GitHub Pages 홈
- `sample.md`: 렌더링 테스트용 샘플 문서
- `_config.yml`: Jekyll 설정
- `.github/workflows/deploy-pages.yml`: push 시 자동 배포 워크플로우

## GitHub 설정 (최초 1회)

1. GitHub 저장소 **Settings → Pages**로 이동
2. **Build and deployment**의 Source를 **GitHub Actions**로 선택
3. 기본 브랜치를 `main`으로 사용한다면, `main`에 push할 때마다 자동 배포됨

> 현재 워크플로우는 `main` 브랜치 push를 기준으로 동작합니다.
> 기본 브랜치가 다르면 `.github/workflows/deploy-pages.yml`의 `on.push.branches` 값을 변경하세요.
