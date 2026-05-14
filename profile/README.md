<h1 align="center">VocaNova</h1>

<p align="center">
  <b>읽다가 만난 영어 단어를, 한 번의 동작으로 모으고 SRS로 복습하세요.</b><br/>
  브라우저 · macOS · iOS — 어디서 모았든 한 곳에서 학습합니다.
</p>

<p align="center">
  <a href="http://vocanova.online/">
    <img src="https://img.shields.io/badge/🌐_Visit_vocanova.online-4F46E5?style=for-the-badge&logoColor=white" alt="vocanova.online" />
  </a>
</p>

<p align="center">
  👉 <a href="http://vocanova.online/"><b>vocanova.online</b></a> 에서 랜딩 페이지와 다운로드 정보를 확인하세요.
</p>

---

## 🌱 VocaNova가 풀려는 문제

공식 문서를 읽다가, 웹서핑을 하다가, PDF 파일을 읽다가, macOS에서 코드를 작성하다가 만나는 **모르는 단어**.
사전 앱을 열고, 검색하고, 단어장에 옮겨 적는 — 그 번거로움 때문에 대부분의 단어는 그대로 흘려보내집니다.

**VocaNova**는 이 번거로움을 0에 가깝게 만듭니다.

- 웹에서는 **드래그 한 번**,
- macOS의 다른 앱에서는 **⌘⇧F 한 번**,
- 그렇게 모은 단어는 **iOS에서 간격 반복(SRS)으로 자동 복습**.

세 가지 클라이언트가 같은 Supabase 백엔드를 공유하기 때문에, 어디서 저장하든 모든 기기에서 즉시 보입니다.

---

## 🧩 제품 구성

| Client | 한 줄 요약 | Repository |
| --- | --- | --- |
| 🌐 **Chrome Extension** | 어떤 웹페이지에서든 드래그 / 더블클릭으로 사전 팝업 + 단어장 저장 | [`voca-extension`](https://github.com/VocaNovaHQ/voca-extension) |
| 🖥️ **macOS App** | 시스템 전역 단축키(⌘⇧F)로 모든 앱에서 사전 호출 — 메뉴바 상주 | [`VocaNovaApp`](https://github.com/VocaNovaHQ/VocaNovaApp) |
| 📱 **iOS App** | 모아둔 단어를 SRS로 복습 · 학습 통계 · 복습 알림 | [`VocaNova`](https://github.com/VocaNovaHQ/VocaNova) |

---

## 🏗️ 아키텍처

```
┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐
│ Chrome Ext.     │   │   macOS App     │   │    iOS App      │
│ (JS · MV3)      │   │ (Swift · AppKit)│   │ (RN · Expo)     │
└────────┬────────┘   └────────┬────────┘   └────────┬────────┘
         │                     │                     │
         │   Naver Dict API ◀──┼──▶ Naver Dict API   │
         │                     │                     │
         └─────────────────────┼─────────────────────┘
                               ▼
                      ┌────────────────────┐
                      │     Supabase       │
                      │  Auth · Postgres   │
                      │  RPC · Realtime    │
                      └────────────────────┘
```

- **단어 source-of-truth**: 네이버 영어 사전 (발음 · 품사별 뜻 · 예문 · 유반의어)
- **데이터 백엔드**: Supabase (Auth · Postgres · PostgREST RPC)
- **인증**: Google / Apple OAuth — 모든 클라이언트에서 동일한 세션
- **동기화**: 한 클라이언트에서 추가한 단어가 즉시 다른 기기에 반영

---

## 🛠️ 기술 스택

<table>
  <tr>
    <td><b>Chrome Extension</b></td>
    <td>Manifest V3 · Vanilla JS · Service Worker · Shadow DOM</td>
  </tr>
  <tr>
    <td><b>macOS</b></td>
    <td>Swift · SwiftUI + AppKit · Accessibility API · XcodeGen</td>
  </tr>
  <tr>
    <td><b>iOS</b></td>
    <td>React Native · Expo SDK 54 · TypeScript · Zustand · NativeWind</td>
  </tr>
  <tr>
    <td><b>Backend</b></td>
    <td>Supabase (Postgres · Auth · PostgREST RPC)</td>
  </tr>
</table>

---

## 🚀 현재 상태

VocaNova는 **활발히 개발 중**입니다. 세 클라이언트 모두 동작하는 프로토타입이 완성되어 있고, 정식 배포(Chrome Web Store · App Store · DMG)를 준비하고 있습니다.

<sub>업데이트 / 배포 링크는 각 리포지토리에서 확인할 수 있습니다.</sub>
