# 배포 가이드 — Cloudflare Pages + ondapspeech.com

호스팅: **Cloudflare Pages** · 도메인: **ondapspeech.com**(후이즈 등록 → Cloudflare 네임서버 이전)
아래는 **브라우저에서 직접** 진행하는 절차입니다. (네임서버 변경·Cloudflare/후이즈 로그인은 본인이 직접)

---

## 0. 사전 상태
- [x] 후이즈 → Cloudflare 네임서버 변경 완료
- [x] og-image.png 생성 완료 → **저장소 루트에 `og-image.png`(1200×630)로 넣고 커밋했는지 확인**
- [ ] GitHub 저장소에 코드 푸시
- [ ] Cloudflare Pages ↔ GitHub 자동배포 연결

---

## 1. Cloudflare에 도메인 추가 (이미 했다면 건너뛰기)
1. Cloudflare 대시보드 → **Add a site** → `ondapspeech.com` 입력 → **Free** 플랜 선택.
2. Cloudflare가 발급한 **네임서버 2개**를 확인.
3. 후이즈(whois) 관리화면 → 네임서버를 위 2개로 교체. → (완료)
4. Cloudflare에서 도메인 상태가 **Active**가 될 때까지 대기(전파 수십 분~수 시간).

## 2. GitHub 저장소 준비
- 코드(`index.html`, `rep.jpg`, `og-image.png`, `README.md`, `DEPLOY.md`)를 GitHub 저장소에 푸시.
- **빌드 산출물이 없는 단일 HTML**이므로 별도 빌드 설정 불필요.

## 3. Cloudflare Pages 프로젝트 생성 (GitHub 연동)
1. Cloudflare 대시보드 → **Workers & Pages** → **Create** → **Pages** 탭 → **Connect to Git**.
2. GitHub 계정 인증 → 이 저장소 선택.
3. 빌드 설정:
   - **Framework preset**: `None`
   - **Build command**: *(비움)*
   - **Build output directory**: `/`  (루트)
4. **Save and Deploy** → 첫 배포 완료되면 `*.pages.dev` 임시 주소로 확인.
> 이후 `main` 브랜치에 푸시할 때마다 **자동 재배포**됩니다.

## 4. 커스텀 도메인 연결
1. 생성된 Pages 프로젝트 → **Custom domains** → **Set up a custom domain**.
2. `ondapspeech.com` 추가 → 안내대로 DNS 레코드 적용(같은 Cloudflare 계정이면 자동).
3. `www.ondapspeech.com` 도 추가.
4. **www → 루트 리다이렉트** 설정:
   - 권장: Cloudflare **Rules → Redirect Rules**에서 `www.ondapspeech.com/*` →
     `https://ondapspeech.com/$1` (301)로 리다이렉트.

## 5. SSL / 접속 확인
- 전파 후 `https://ondapspeech.com` 접속 → 자물쇠(SSL) 정상 확인.
- `http://` 및 `www.` 접속이 `https://ondapspeech.com`으로 모이는지 확인.

## 6. 공유 미리보기(OG) 확인
- 카카오톡 채팅에 링크 붙여넣어 카드(제목·설명·이미지) 표시 확인.
- 안 뜨거나 이전 이미지가 보이면 캐시 갱신:
  - **카카오**: 카카오 디버거 — https://developers.kakao.com/tool/debugger/sharing
  - **페이스북**: Sharing Debugger — https://developers.facebook.com/tools/debug/ → **Scrape Again**
- 점검 포인트: `og:image`가 `https://ondapspeech.com/og-image.png` 로 200 응답인지(루트에 파일 존재해야 함).

---

## 체크리스트
- [ ] 저장소 루트에 `index.html` + `og-image.png`(1200×630) 존재
- [ ] GitHub 푸시 완료
- [ ] Cloudflare Pages ↔ GitHub 연결 + 자동배포 동작
- [ ] `ondapspeech.com` Active + SSL
- [ ] `www` → 루트 301 리다이렉트
- [ ] 카카오/페북 공유 카드 정상
