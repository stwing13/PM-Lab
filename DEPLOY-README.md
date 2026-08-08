# PM Lab — 프로젝트 관리 실습 콘솔

PMBOK 6th 기반 프로젝트 관리 실습 웹앱입니다. 착수 → 계획 → 실행 → 감시·통제 → 종료의 전 과정을 브라우저에서 실습합니다. 별도 서버·데이터베이스 없이 동작하는 **단일 정적 사이트**이며, 실습 데이터는 사용자 브라우저에 저장됩니다.

## 구성

```
.
├── index.html     # 앱 본체 (단일 파일, 모든 로직·스타일 포함)
├── _headers       # Cloudflare Pages 보안·캐싱 헤더
├── .gitignore
└── README.md
```

빌드 단계가 없습니다. `index.html`을 그대로 서빙하면 됩니다.

## GitHub + Cloudflare Pages 배포

### 1단계 — GitHub 저장소에 올리기

새 저장소를 만든 뒤 이 폴더의 파일을 커밋·푸시합니다.

```bash
git init
git add .
git commit -m "Initial commit: PM Lab"
git branch -M main
git remote add origin https://github.com/<사용자명>/<저장소명>.git
git push -u origin main
```

### 2단계 — Cloudflare Pages에서 연결

1. Cloudflare 대시보드 → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. 방금 만든 GitHub 저장소를 선택하고 **Begin setup**
3. 빌드 설정을 아래와 같이 지정합니다.

   | 항목 | 값 |
   |------|-----|
   | Production branch | `main` |
   | Framework preset | `None` |
   | Build command | *(비움)* |
   | Build output directory | `/` |

4. **Save and Deploy**를 누르면 배포가 시작됩니다.

배포가 끝나면 `https://<프로젝트명>.pages.dev` 주소로 접속할 수 있습니다.

### 3단계 — 자동 재배포

GitHub `main` 브랜치에 새 커밋을 푸시할 때마다 Cloudflare Pages가 자동으로 다시 배포합니다. 앱을 수정하려면 `index.html`을 고쳐 커밋·푸시하면 됩니다.

```bash
git add index.html
git commit -m "Update: <변경 내용>"
git push
```

## 사용자 지정 도메인 (선택)

Pages 프로젝트 → **Custom domains** → **Set up a custom domain**에서 보유한 도메인을 연결할 수 있습니다. 도메인이 Cloudflare에서 관리 중이면 DNS 레코드가 자동으로 추가됩니다.

## 참고

- 실습 데이터는 브라우저 저장소에 보관되므로, 사용자별·기기별로 독립적입니다. 서버에 저장되지 않습니다.
- 앱 우측 상단 **내보내기**로 프로젝트를 JSON 파일로 저장할 수 있습니다.
