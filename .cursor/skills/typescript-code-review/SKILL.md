---
name: typescript-code-review
description: >-
  Reviews TypeScript and TSX changes for type safety, correctness, async/error
  handling, API boundaries, tests, and security. Use when reviewing PRs or
  diffs, when the user asks for a TypeScript code review, or when analyzing
  .ts/.tsx/.mts changes in Node, browser, or React codebases.
---

# TypeScript 코드 리뷰

## 적용 시점

- `.ts`, `.tsx`, `.mts`, `.cts` 또는 `tsconfig`에 영향을 주는 변경이 있을 때
- 사용자가 PR/diff/파일에 대한 **코드 리뷰**를 요청할 때
- `pm-code-reviewer` 에이전트가 리뷰를 수행할 때

## 워크플로

1. **맥락**: 변경 목적, 관련 이슈/요구사항이 있으면 먼저 요약한다.
2. **범위**: 리뷰 대상 파일과 공개 API(export) 경계를 식별한다.
3. **점검**: 아래 체크리스트와 [reference.md](reference.md)의 상세 항목을 적용한다.
4. **출력**: 이 문서의 **리뷰 결과 형식**으로만 정리한다(중복 서술 최소화).

## 빠른 체크리스트

- [ ] 타입: `any`/`as` 남용, 잘못된 단언, 빈 약한 타입
- [ ] 제어 흐름: null/undefined, 배열·객체 접근, exhaustiveness(`never`)
- [ ] 비동기: 누락된 `await`, 잘못된 Promise 병렬/순서, 에러 전파
- [ ] 경계: 외부 입력 검증, 파싱/직렬화, 공개 API 시그니처 안정성
- [ ] 리소스: 이벤트 리스너/타이머/스트림 정리
- [ ] 보안: 인젝션, 민감 로그, 인증/인가 가정
- [ ] 테스트: 회귀·엣지 케이스, 타입과 런타임 불일치 가능 지점

## 리뷰 결과 형식

다음 섹션 순서를 유지한다. 해당 없음은 "없음"으로 짧게 표기한다.

```markdown
## 요약
[한두 문장으로 변경의 품질과 머지 가능 여부]

## 강점
- ...

## 이슈
### Critical (머지 전 수정)
- [파일:줄] ...

### Major (가능하면 본 PR에서)
- ...

### Minor / 제안
- ...

## 질문 / 가정
- ...

## 체크리스트 메모
[위 빠른 체크리스트 중 특히 확인한 항목만 bullet]
```

## 심각도 기준

- **Critical**: 런타임 예외, 보안 취약점, 데이터 손상, 잘못된 타입으로 인한 거짓 안전
- **Major**: 유지보수·확장 시 높은 비용, 명백한 API 혼란, 테스트 부재로 회귀 위험
- **Minor**: 가독성, 네이밍, 작은 리팩터 제안(동작 동일)

## 추가 자료

- 세부 기준·패턴: [reference.md](reference.md)
