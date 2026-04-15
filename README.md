# 🔗 My URL Shortener (100% Free)

GitHub Pages만 사용하는 완전 무료 단축 URL 서비스. 서버/DB 없음.

## 동작 원리

- `urls.json` 에 `{ "slug": "원본URL" }` 매핑 저장
- GitHub Pages가 `/slug` 요청 시 `404.html` 반환 → JS가 `urls.json` 읽어서 redirect
- 관리 UI(`index.html`)에서 GitHub API로 `urls.json` 을 수정 → 자동 배포

## 초기 설정

### 1. GitHub 저장소 만들기
1. GitHub에서 **Public** 저장소 생성 (예: `url-shortener`)
2. 이 폴더의 파일들을 저장소에 업로드/푸시

### 2. GitHub Pages 활성화
- 저장소 → **Settings** → **Pages**
- Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → Save
- 몇 분 후 `https://<username>.github.io/url-shortener/` 에서 접속 가능

### 3. Personal Access Token (PAT) 발급
- GitHub → 우상단 프로필 → **Settings** → **Developer settings**
- **Personal access tokens** → **Tokens (classic)** → **Generate new token (classic)**
- Scope: **repo** 체크 (Private 저장소면 필수, Public이어도 쓰기엔 필요)
- 만료기간 설정 후 생성 → 토큰 복사 (한 번만 표시됨)

### 4. 관리 페이지에서 설정
- `https://<username>.github.io/url-shortener/` 접속
- 사용자명 / 저장소명 / 브랜치 / PAT 입력 → **저장**
- **목록 불러오기** 클릭
- 원본 URL 입력 후 **추가하기**

## 사용 예시

- 원본: `https://www.some-very-long-url.com/path/to/something?q=abc`
- 단축: `https://<username>.github.io/url-shortener/blog`

## 주의사항

- 저장소는 **Public**이어야 `urls.json` 을 익명으로 fetch 가능 (redirect 동작). Private으로 하려면 토큰이 필요해 단축 URL 사용 자체가 복잡해짐.
- PAT는 브라우저 **localStorage**에만 저장됨 (외부 전송 없음). 공용 PC에서 사용하지 말 것.
- URL 추가 후 GitHub Pages 재배포에 **30초~2분** 소요.
- `.com` 같은 짧은 도메인 원하면 도메인 구매 후 GitHub Pages Custom Domain 기능으로 연결 (연 1~2만원).
