# HSLog Project Structure

## 1. Overview

HSLog는 Monorepo 구조로 관리한다.

초기에는 Web과 API를 분리하여 구성하며, 공통으로 사용할 수 있는 게임 로직은 별도 Package로 관리한다.

Backend는 초기 MVP에서 최소한으로 유지한다.

다만 향후 커뮤니티, 사용자 계정, 랭킹 등의 기능이 추가될 수 있으므로 확장 가능한 구조를 유지한다.

---

# 2. Repository Structure

```text
hslog/
├── apps/
│   ├── web/
│   └── api/
│
├── packages/
│   └── game/
│
├── data/
│
├── scripts/
│
├── docs/
│
├── package.json
├── turbo.json
└── README.md
```

---

# 3. Apps

실행 가능한 애플리케이션은 `apps`에서 관리한다.

```text
apps/
├── web/
└── api/
```

---

## 3.1 Web

`apps/web`은 사용자에게 제공되는 메인 웹 애플리케이션이다.

Next.js를 사용한다.

주요 역할:

- 게임 UI
- 카드 비교
- SEO 페이지
- 다국어 UI
- 사용자 인터랙션

예상 구조:

```text
apps/web/
├── app/
├── components/
├── features/
├── lib/
└── public/
```

세부 구조는 실제 개발 과정에서 조정한다.

---

## 3.2 API

`apps/api`는 향후 서버 기능을 담당한다.

초기 MVP에서는 최소한의 구조만 유지한다.

향후 다음 기능이 필요해질 경우 확장한다.

- Authentication
- User
- Ranking
- Community
- Posts
- Comments
- Likes

현재 필요하지 않은 기능을 미리 구현하지 않는다.

---

# 4. Packages

여러 애플리케이션에서 공유할 가능성이 있는 코드만 `packages`로 분리한다.

초기에는 게임 도메인 로직을 관리하는 `game` Package만 생성한다.

```text
packages/
└── game/
```

---

## 4.1 Game

게임 규칙과 UI에 의존하지 않는 게임 로직을 관리한다.

예:

```text
packages/game/
├── src/
│   ├── generateGame
│   ├── generateRound
│   ├── validateAnswer
│   └── types
│
└── package.json
```

주요 책임:

- 카드 비교
- 출시일 비교
- 게임 시작 데이터 생성
- 다음 라운드 생성
- 정답 판정

React나 Next.js에 직접 의존하지 않는다.

---

# 5. Data

게임에서 사용하는 정적 데이터는 `data`에서 관리한다.

```text
data/
├── cards/
└── sets/
```

예:

```text
data/
├── cards.json
└── sets.json
```

원본 데이터는 hsdata를 참고한다.

게임에서 사용할 수 있도록 가공된 데이터만 관리한다.

상세 데이터 정책은 `data-source.md`를 따른다.

---

# 6. Scripts

데이터 생성이나 업데이트와 같은 개발용 스크립트를 관리한다.

```text
scripts/
└── update-data/
```

예:

- hsdata 데이터 읽기
- 필요한 카드 필드 추출
- set 데이터 정리
- 출시일 정보 연결
- 게임용 데이터 생성

스크립트는 Web Application과 분리한다.

---

# 7. Docs

프로젝트의 주요 정책과 설계 문서를 관리한다.

```text
docs/
├── product-overview.md
├── game-rules.md
├── data-source.md
├── ui-ux.md
├── architecture.md
└── project-structure.md
```

문서는 프로젝트의 방향과 중요한 결정 사항을 기록한다.

구체적인 구현 과정에서 계속 변경될 수 있는 내용까지 과도하게 문서화하지 않는다.

---

# 8. Future Expansion

프로젝트가 성장하면서 실제 필요가 생길 경우 구조를 확장한다.

예:

```text
packages/
├── game/
├── shared/
└── ui/
```

또는:

```text
apps/
├── web/
├── api/
└── admin/
```

다만 현재 요구되지 않는 구조는 미리 생성하지 않는다.

---

# 9. Structure Principles

HSLog의 프로젝트 구조는 다음 원칙을 따른다.

### Keep It Simple

현재 필요한 구조만 만든다.

### Separate Responsibilities

Web, API, Game Logic, Data의 역할을 분리한다.

### Share Only When Needed

실제로 공유되는 코드만 Package로 분리한다.

### Expand When Necessary

미래를 고려하되 미래의 모든 기능을 미리 구현하지 않는다.

---

# 10. Summary

초기 HSLog는 다음 구조를 기준으로 시작한다.

```text
apps
├── web        # Next.js
└── api        # Future Backend

packages
└── game       # Shared Game Logic

data           # Game Dataset

scripts        # Data Processing

docs           # Project Documentation
```

현재는 게임 경험을 빠르게 구현하는 것을 우선한다.

Backend와 추가 Package는 실제 요구사항이 발생할 때 확장한다.
