# 온답스피치 ONDAP Speech — 랜딩페이지

광주·전남 학생 대상 입시·면접·발표 컨설팅 브랜드 단일 페이지.

## 구조
- 빌드 과정 없는 **순수 HTML 단일 파일**(`index.html`, 인라인 CSS/JS).
- 에셋: `rep.jpg`(대표 사진, 세로 4:5 — 현재 800×1000), `og-image.png`(SNS 공유 카드, 1200×630).
- 호스팅: **Cloudflare Pages** / 도메인: **ondapspeech.com**
- 배포 절차는 [`DEPLOY.md`](DEPLOY.md) 참고.

## ⚠️ 필요 파일 — og-image.png
> **루트에 `og-image.png`(1200×630) 필요.**
> `index.html`의 OG 메타가 `https://ondapspeech.com/og-image.png`를 가리키므로,
> 이 파일이 저장소 루트에 있어야 카카오톡·페이스북 공유 미리보기 카드가 표시됩니다.
> 아직 추가되지 않았다면 1200×630 이미지를 루트에 `og-image.png`로 넣고 커밋하세요.

## 설정 변경 (CONFIG)
전화/카카오/문의폼 연결은 `index.html` 하단 `<script>`의 `CONFIG` 객체만 수정하면 됩니다.
- `phone` — 상담 전화번호
- `kakao` — 카카오톡 채널 URL
- `orgInquiry` — 기관 문의폼 URL(비우면 전화로 연결)
- `personalInquiry` — 개인 상담 채널(비우면 카카오로 연결)

## 로컬 미리보기
같은 폴더에서 정적 서버를 띄워 확인(파일 직접 열기 시 OG 이미지 등 일부 동작이 다를 수 있음).
