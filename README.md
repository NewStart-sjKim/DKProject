# Gulp 웹 퍼블리싱 프로젝트 (레이아웃 시스템)

Gulp와 gulp-file-include를 사용한 웹 퍼블리싱 자동화 프로젝트입니다.
레이아웃 시스템으로 Header/Footer를 공통 관리합니다.

## 📁 프로젝트 구조

```
WebPublisherAssignment/
├── project/
│   ├── src/                      # ✨ 소스 파일 (여기서 작업!)
│   │   ├── index.html           # 메인 페이지
│   │   ├── layouts/             # 레이아웃 템플릿 (참고용)
│   │   │   └── default.html    
│   │   ├── partials/            # 공통 레이아웃 요소
│   │   │   ├── header.html     # 헤더 (모든 페이지 공통)
│   │   │   └── footer.html     # 푸터 (모든 페이지 공통)
│   │   ├── components/          # 🎨 재사용 가능한 컴포넌트
│   │   │   ├── hero-section.html
│   │   │   ├── page-list.html
│   │   │   ├── card.html
│   │   │   └── button-group.html
│   │   ├── pages/               # 서브 페이지들
│   │   │   ├── status/
│   │   │   │   └── isList.html
│   │   │   └── wsg/
│   │   │       └── list.html
│   │   ├── css/                 # CSS 파일
│   │   │   └── style.css
│   │   ├── js/                  # JavaScript 파일
│   │   │   └── main.js
│   │   ├── images/              # 이미지 파일
│   │   ├── fonts/               # 폰트 파일
│   │   └── COMPONENTS.md        # 컴포넌트 사용 가이드
│   │
│   └── dest/                     # 🚀 출력 결과물 (Gulp가 자동 생성)
│       ├── index.html           # 빌드된 메인 페이지
│       ├── pages/               # 빌드된 서브 페이지들
│       ├── css/                 # 처리된 CSS
│       ├── js/                  # 번들링된 JS
│       ├── images/              # 최적화된 이미지
│       └── fonts/               # 폰트
│
├── gulpfile.js                  # Gulp 설정 파일
└── package.json                 # 프로젝트 의존성
```

## 🎨 컴포넌트 시스템 사용법

### 시스템 구조

프로젝트는 3개의 레이어로 구성됩니다:

1. **Partials** (`src/partials/`) - 공통 레이아웃 (header, footer)
2. **Components** (`src/components/`) - 재사용 가능한 UI 컴포넌트
3. **Pages** (`src/` & `src/pages/`) - 실제 페이지

### 기본 페이지 구조

```html
<!-- src/index.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
  <title>페이지 제목</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <!-- Header 포함 -->
  @@include('partials/header.html')

  <!-- Main Content -->
  <main>
    <!-- 컴포넌트 사용 -->
    @@include('components/hero-section.html')
    @@include('components/page-list.html')
  </main>

  <!-- Footer 포함 -->
  @@include('partials/footer.html')

  <script src="js/main.js"></script>
</body>
</html>
```

### 컴포넌트 사용 방법

#### 1️⃣ 기본 사용 (변수 없이)
```html
@@include('components/hero-section.html')
```

#### 2️⃣ 변수와 함께 사용
```html
@@include('components/card.html', {
  "title": "카드 제목",
  "description": "카드 설명입니다.",
  "link": "#",
  "buttonText": "자세히 보기"
})
```

#### 3️⃣ 여러 번 재사용
```html
<main>
  @@include('components/card.html', {"title": "첫 번째", ...})
  @@include('components/card.html', {"title": "두 번째", ...})
  @@include('components/card.html', {"title": "세 번째", ...})
</main>
```

> 📖 **자세한 컴포넌트 가이드**: `project/src/COMPONENTS.md` 참고

## 🚀 시작하기

### 1. 의존성 설치

```bash
npm install
```

### 2. 개발 모드 실행

```bash
npm run dev
```

또는

```bash
gulp dev
```

이 명령어는:
- HTML 파일 include 처리 및 빌드
- CSS 파일에 Autoprefixer 적용
- JavaScript 파일 번들링
- BrowserSync로 로컬 서버 시작 (http://localhost:3000)
- 파일 변경 감지 및 자동 새로고침

### 3. 배포용 빌드

```bash
npm run build
```

또는

```bash
gulp build
```

이 명령어는:
- 모든 파일 처리
- CSS 및 JavaScript 압축
- 이미지 최적화
- 배포 준비 완료 파일 생성

## 📝 사용 가능한 Gulp 태스크

- `gulp html` - HTML 파일 include 처리
- `gulp styles` - CSS 처리 (Autoprefixer)
- `gulp scripts` - JavaScript 번들링
- `gulp images` - 이미지 최적화
- `gulp fonts` - 폰트 파일 복사
- `gulp watch` - 파일 변경 감지 및 BrowserSync 실행
- `gulp clean` - 빌드 폴더 정리
- `gulp dev` - 개발 모드 (기본값)
- `gulp build` - 배포용 빌드

## 🛠️ 주요 기능

### HTML 처리 (gulp-file-include)
- **레이아웃 시스템** - 공통 레이아웃 관리
- **컴포넌트 재사용** - Header, Footer 등 부분 템플릿
- **변수 지원** - 페이지별 title, meta 등 커스터마이징

### CSS 처리
- **Autoprefixer** - 자동 브라우저 호환성 접두사
- **Sourcemaps** - 디버깅용
- **CSS 압축** - 배포용 최적화

### JavaScript 처리
- **파일 번들링** - 여러 JS 파일을 하나로 합치기
- **Sourcemaps** - 디버깅용
- **압축** - 배포용 최적화

### 이미지 최적화
- PNG, JPG, GIF, SVG 자동 최적화
- 용량 감소

### 개발 서버
- **BrowserSync** - 실시간 새로고침
- **포트**: 3000

## 💡 작업 흐름

### 📝 새 페이지 만들기

1. `project/src/pages/`에 새 HTML 파일 생성
2. 레이아웃 선언 및 변수 설정
3. Body 내용 작성
4. Gulp가 자동으로 `project/dest/pages/`에 완성된 HTML 생성

### 🎯 공통 요소 수정하기

- **Header 수정**: `src/partials/header.html` 편집
- **Footer 수정**: `src/partials/footer.html` 편집
- **레이아웃 수정**: `src/layouts/default.html` 편집

→ 한 번만 수정하면 모든 페이지에 자동 반영!

### 🚀 Gulp가 자동으로 처리

1. `src/` 폴더의 파일 변경 감지
2. HTML: include 처리 후 `dest/`로 빌드
3. CSS: Autoprefixer 적용 + 압축 → `dest/css/`
4. JS: 번들링 + 압축 → `dest/js/`
5. 이미지: 최적화 → `dest/images/`
6. 브라우저 자동 새로고침

## 📦 설치된 패키지

- `gulp` - 태스크 러너
- `gulp-file-include` - HTML 레이아웃 시스템
- `gulp-autoprefixer` - CSS 벤더 프리픽스
- `gulp-clean-css` - CSS 압축
- `gulp-uglify` - JavaScript 압축
- `gulp-concat` - 파일 병합
- `gulp-rename` - 파일명 변경
- `gulp-imagemin` - 이미지 최적화
- `gulp-sourcemaps` - 소스맵 생성
- `browser-sync` - 개발 서버 및 자동 새로고침
- `del` - 파일/폴더 삭제

## 🎯 레이아웃 시스템의 장점

1. **코드 재사용** - Header, Footer를 모든 페이지에서 공유
2. **유지보수 쉬움** - 한 곳만 수정하면 모든 페이지에 반영
3. **일관성 유지** - 모든 페이지가 동일한 구조 유지
4. **개발 속도 향상** - body 내용만 작성하면 됨
5. **빌드 타임에 처리** - 런타임 성능 저하 없음

## 📄 라이선스

MIT
