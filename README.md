# 환율 & 가계부 통합 웹앱

이 프로젝트는 **환율 계산기**와 **가계부 기능**을 하나로 통합한 웹 애플리케이션입니다.
모바일 반응형 디자인으로, 로그인 없이 환율 확인이 가능하며, 로그인 시 지출 내역을 저장할 수 있는 **개인 맞춤 가계부** 기능을 제공합니다.

## 🔧 주요 기능

### 💱 환율 탭 (기본 탭)

* 기준 통화 선택 가능 (KRW, USD, EUR 등 10개)
* 실시간 환율 데이터 (exchangerate.host API)
* 입력 금액 → 주요 통화로 환산
* 환산된 금액 기준으로 금액 구간별 소비 예시 제공 (예: 쌀국수, 커피 등)
* 로그인 없이 사용 가능

### 🧾 가계부 탭 (로그인 필요)

* 수동 회원가입 (이메일, 비밀번호, 닉네임, 주요 통화)
* 로그인/로그아웃 기능 (Firebase Auth)
* 지출 내역 입력 및 저장 (Firestore)
* 사용자별 지출 내역만 접근 가능 (보안 규칙 설정됨)

## 📦 기술 스택

* HTML, CSS, JavaScript
* Firebase Hosting (선택)
* Firebase Authentication
* Firebase Firestore
* exchangerate.host API (무료, API Key 불필요)

## 📁 파일 구성

* `index.html` — 전체 기능이 통합된 단일 HTML 파일
* `README.md` — 프로젝트 설명 파일 (현재 문서)

## 🛡 보안 설정 (Firestore Rules)

```js
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {

    match /expenses/{docId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.uid;
    }

    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## 🚀 배포하기

1. GitHub에 `index.html` 업로드
2. Vercel에 GitHub Repo 연결
3. (선택) Firebase Hosting에 배포

## ✅ 사용 예시

* 한국인이 자주 가는 국가 통화로 환산 (VND, JPY, THB 등)
* “₩1,000 = 쌀국수 한 그릇” 같은 금액별 소비 예시 확인
* 개인 지출내역 관리 & 로그인 시 지속 저장

---

> 💡 커스터마이징이나 기능 추가 (통계 차트, 월간 분석 등)이 필요하다면 언제든 확장 가능!
