# Google AdSense 설정 가이드

이 가이드는 사이트에 Google AdSense를 설정하는 방법을 설명합니다.

## 1. Google AdSense 계정 생성 및 승인

1. [Google AdSense](https://www.google.com/adsense) 방문
2. Google 계정으로 로그인
3. 웹사이트 URL 입력: `https://atooooomic.github.io`
4. AdSense 정책을 검토하고 동의
5. 계정 정보 입력 (주소, 전화번호 등)
6. 사이트 승인 대기 (일반적으로 며칠 소요)

## 2. Publisher ID 확인

1. [AdSense 계정](https://www.google.com/adsense)에 로그인
2. **계정** > **설정** > **계정 정보**로 이동
3. **게시자 ID**를 확인 (형식: `ca-pub-xxxxxxxxxxxxxxxx`)

## 3. 환경 변수 설정

`.env` 파일에 Publisher ID를 추가:

```bash
PUBLIC_GOOGLE_ADSENSE_ID=ca-pub-xxxxxxxxxxxxxxxx
```

**참고:** `.env` 파일은 Git에 커밋되지 않습니다. 로컬 개발 환경에만 존재합니다.

## 4. 프로덕션 환경 설정 (GitHub Pages)

GitHub Actions를 사용하는 경우:

1. GitHub 저장소 설정으로 이동
2. **Settings** > **Secrets and variables** > **Actions**
3. **New repository secret** 클릭
4. Name: `PUBLIC_GOOGLE_ADSENSE_ID`
5. Value: `ca-pub-xxxxxxxxxxxxxxxx`
6. **Add secret** 클릭

## 5. 광고 단위 생성

1. AdSense 대시보드에서 **광고** > **광고 단위별** 선택
2. **디스플레이 광고** 클릭
3. 광고 이름 입력 (예: "Article Top", "Sidebar")
4. 광고 크기 선택:
   - **반응형**: 자동으로 크기 조정 (권장)
   - **고정**: 특정 크기 지정
5. **만들기** 클릭
6. **광고 슬롯 ID** 복사 (형식: `1234567890`)

## 6. 광고 배치

### 방법 1: 컴포넌트 사용 (권장)

블로그 포스트나 페이지에 `AdSense` 컴포넌트 추가:

```astro
---
import AdSense from "@/components/AdSense.astro";
---

<AdSense slot="1234567890" />
```

#### Props 옵션:

```astro
<AdSense
  slot="1234567890"          <!-- 필수: 광고 슬롯 ID -->
  format="auto"              <!-- 선택: 광고 형식 (auto, rectangle, horizontal, vertical) -->
  responsive={true}          <!-- 선택: 반응형 여부 (기본값: true) -->
  className="my-custom-ad"   <!-- 선택: 커스텀 CSS 클래스 -->
/>
```

### 방법 2: 수동 배치

직접 HTML 코드 삽입:

```html
<ins
  class="adsbygoogle"
  style="display:block"
  data-ad-client="ca-pub-xxxxxxxxxxxxxxxx"
  data-ad-slot="1234567890"
  data-ad-format="auto"
  data-full-width-responsive="true"
></ins>
<script>
  (adsbygoogle = window.adsbygoogle || []).push({});
</script>
```

## 7. 광고 배치 권장 위치

### 블로그 포스트:
- 제목 바로 아래 (상단)
- 첫 번째 단락 후
- 본문 중간
- 포스트 끝 (관련 포스트 전)

### 메인 페이지:
- 사이드바
- 포스트 목록 사이

### 예시 (PostDetails.astro):

```astro
---
import AdSense from "@/components/AdSense.astro";
---

<article>
  <h1>{title}</h1>

  <!-- 상단 광고 -->
  <AdSense slot="1234567890" format="horizontal" />

  <div class="content">
    <!-- 본문 내용 -->
  </div>

  <!-- 하단 광고 -->
  <AdSense slot="0987654321" />
</article>
```

## 8. 테스트 및 확인

1. 로컬 개발 환경에서 테스트:
   ```bash
   npm run dev
   ```

2. 광고 공간이 표시되는지 확인
   - 처음에는 빈 공간이나 플레이스홀더가 표시될 수 있음
   - AdSense 승인 전에는 광고가 표시되지 않음

3. 프로덕션 배포:
   ```bash
   npm run build
   git add .
   git commit -m "Add Google AdSense"
   git push
   ```

4. AdSense 대시보드에서 광고 상태 확인

## 9. AdSense 정책 준수

반드시 지켜야 할 사항:

- ❌ 자신의 광고 클릭 금지
- ❌ 광고 클릭을 유도하는 문구 금지 ("광고를 클릭하세요")
- ❌ 성인, 폭력, 불법 콘텐츠 금지
- ✅ 원본 콘텐츠 제공
- ✅ 페이지당 적절한 광고 수 (과도한 광고 금지)

자세한 내용: [AdSense 프로그램 정책](https://support.google.com/adsense/answer/48182)

## 10. 문제 해결

### 광고가 표시되지 않는 경우:

1. **환경 변수 확인**
   - `.env` 파일에 `PUBLIC_GOOGLE_ADSENSE_ID`가 올바르게 설정되었는지 확인

2. **AdSense 승인 대기**
   - 새 사이트는 승인까지 며칠이 걸릴 수 있음
   - AdSense 대시보드에서 승인 상태 확인

3. **광고 코드 확인**
   - 브라우저 개발자 도구(F12) > Console 탭에서 에러 확인
   - `data-ad-client`와 `data-ad-slot` 값이 올바른지 확인

4. **광고 차단기**
   - 브라우저의 광고 차단 확장 프로그램 비활성화

5. **트래픽**
   - 트래픽이 낮으면 광고가 제한적으로 표시될 수 있음

### 수익이 발생하지 않는 경우:

- 실제 방문자 트래픽이 있어야 수익 발생
- 일반적으로 며칠 후부터 데이터가 표시됨
- 광고 클릭률(CTR)과 페이지 뷰(PV)가 중요

## 참고 자료

- [Google AdSense 고객센터](https://support.google.com/adsense)
- [AdSense 시작하기](https://support.google.com/adsense/answer/6084409)
- [광고 코드 구현](https://support.google.com/adsense/answer/9274634)
