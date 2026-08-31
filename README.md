# [프로젝트 2] 자유 주제 자동화 설계 및 구현 보고서

## 1. 프로젝트 개요

본 프로젝트에서는 **뉴스레터/블로그 RSS 피드에서 부동산 관련 새 글을 자동으로 수집하고, Google Sheets에 정리하는 자동화 워크플로우**를 구현하였다.

RSS 피드에 새 글이 등록되면 Zapier가 이를 감지하고, 글 제목에 **“부동산”** 키워드가 포함된 경우에만 Google Sheets로 저장되도록 구성하였다.

---

## 2. 최종 결과물

### 2.1 자동화할 반복 업무 정의

| 항목 | 내용 |
|---|---|
| 반복 업무명 | 부동산 관련 뉴스/블로그 업데이트 소식 자동 수집 |
| 기존 방식 | RSS 또는 뉴스 사이트를 직접 확인한 뒤, 필요한 기사 제목과 링크를 수동으로 Google Sheets에 정리 |
| 문제점 | 반복적인 확인 작업이 필요하고, 중요한 부동산 관련 소식을 놓칠 수 있음 |
| 자동화 목표 | RSS 피드에 새 글이 올라오면 자동으로 감지하고, 제목에 “부동산”이 포함된 글만 Google Sheets에 저장 |

---

### 2.2 자동화 도구 선정

#### 선정 도구: **Zapier**

#### 선정 이유

Zapier를 선정한 이유는 다음과 같다.

1. **RSS by Zapier 기능 제공**
   - RSS 피드의 새 항목을 자동으로 감지할 수 있다.

2. **Google Sheets 연동이 간단함**
   - 수집한 데이터를 스프레드시트 또는 행 단위로 쉽게 저장할 수 있다.

3. **Filter by Zapier 제공**
   - 제목에 특정 키워드가 포함된 경우에만 다음 단계가 실행되도록 조건 처리가 가능하다.

4. **코드 없이 워크플로우 구현 가능**
   - 트리거, 필터, 액션을 시각적으로 연결할 수 있어 구현 난이도가 낮다.

---

## 3. 워크플로우 설계 문서

### 3.1 전체 워크플로우 구조

```text
[Trigger]
RSS by Zapier
- New Item in Feed
- RSS 피드에 새 글이 올라오면 자동 실행

        ↓

[Filter]
Filter by Zapier
- 조건: RSS 글 제목 Title에 "부동산" 포함 여부 확인
- 조건을 만족할 때만 다음 단계 진행

        ↓

[Action 1]
Google Sheets
- Create Spreadsheet
- 부동산 관련 데이터를 저장할 스프레드시트 생성

        ↓

[Action 2]
Google Sheets
- Create Spreadsheet Row
- 제목, 링크, 발행일, 작성자 정보를 행으로 추가
```

---

### 3.2 단계별 설명

| 단계 | 앱/기능 | 역할 |
|---|---|---|
| 1 | RSS by Zapier - New Item in Feed | RSS 피드에 새 글이 올라오면 자동화 시작 |
| 2 | Filter by Zapier - Filter conditions | 글 제목에 “부동산” 키워드가 포함된 경우만 통과 |
| 3 | Google Sheets - Create Spreadsheet | 결과를 저장할 Google Sheets 스프레드시트 생성 |
| 4 | Google Sheets - Create Spreadsheet Row | RSS 글 정보를 Google Sheets 행으로 추가 |

---

## 4. 구현 화면 캡처

### 4.1 전체 구현 화면

이미지에서 확인되는 워크플로우는 다음과 같다.

```text
1. RSS by Zapier - New Item in Feed
2. Filter by Zapier - Filter conditions
3. Google Sheets - Create Spreadsheet
4. Google Sheets - Create Spreadsheet Row
```

해당 화면에서는 **Trigger 1개, Filter 1개, Action 2개**가 연결되어 있다.

---

### 4.2 Filter 조건 설정 화면

Filter 조건은 다음과 같이 설정되어 있다.

```text
Only continue if...

1. Title
contains
부동산
```

즉, RSS 피드에서 가져온 글 제목에 **“부동산”**이라는 단어가 포함되어 있을 때만 Google Sheets 관련 액션이 실행된다.

---

### 4.3 Google Sheets 행 추가 설정 화면

Google Sheets의 `Create Spreadsheet Row` 단계에서는 RSS 피드에서 가져온 데이터를 다음 항목에 매핑하였다.

| Google Sheets 필드 | 매핑된 RSS 데이터 |
|---|---|
| Title | RSS 글 제목 |
| Link | RSS 글 링크 |
| Pub Date | 발행일 |
| Author | 작성자 |

예시로 화면에서 다음과 같은 값이 확인된다.

```text
Title: 최대 29조 '삼성 사내대출'...경기 남부 집값 흔들다
Link: RSS 글 링크
Pub Date: 발행일
Author: 김소윤
```

---

## 5. 실행 결과 화면 캡처

### 5.1 실행 시도 결과

제시된 이미지에서 Zap 실행 결과로 다음 메시지가 확인된다.

```text
Zap run failed
We couldn't find any new feeds.
```

이는 워크플로우 구성 오류라기보다는, **실행 시점에 RSS 피드에서 새로 감지할 항목이 없어서 발생한 메시지**로 해석할 수 있다.

즉, 현재 자동화 구조는 구성되어 있으나, 수동 실행 시점에 Zapier가 새 RSS 항목을 찾지 못해 전체 실행이 완료되지 않았다.

---

### 5.2 실행 결과 해석

| 항목 | 결과 |
|---|---|
| 워크플로우 구성 | 완료 |
| Trigger 설정 | 완료 |
| Filter 설정 | 완료 |
| Google Sheets Action 설정 | 완료 |
| 수동 Run 실행 결과 | 신규 RSS 항목 없음으로 실패 메시지 발생 |
| 자동 실행 가능성 | RSS에 새 항목이 발생하면 자동 실행 가능 |

---

## 6. 기능 요구 사항 충족 여부

### 6.1 공통 요구 사항 검토

| 요구사항 | 충족 여부 | 근거 |
|---|---:|---|
| 실제 동작하는 자동화 워크플로우 구현 | 부분 충족 | Zap이 구성되어 있고 활성화되어 있으나, 실행 화면에서는 신규 RSS 항목이 없어 실패 메시지가 표시됨 |
| Trigger 1개 이상 포함 | 충족 | `RSS by Zapier - New Item in Feed` |
| Action 2개 이상 포함 | 충족 | `Google Sheets - Create Spreadsheet`, `Google Sheets - Create Spreadsheet Row` |
| 조건 분기 또는 Filter 1개 이상 포함 | 충족 | `Filter by Zapier - Filter conditions` |
| 조건 경로 실행 결과 확인 | 보완 필요 | Filter 조건은 확인되지만, 실제 통과 후 Google Sheets에 저장된 성공 결과 캡처는 추가하면 더 명확함 |

---

### 6.2 프로젝트 2 요구 사항 검토

| 요구사항 | 충족 여부 | 설명 |
|---|---:|---|
| 자동화할 반복 업무 1개 정의 | 충족 | 부동산 관련 RSS 글 자동 수집 업무 정의 |
| 도구 1개 선정 및 선정 이유 작성 | 충족 | Zapier 선정 및 이유 작성 |
| 자동 실행 구조 구현 | 충족 | RSS 새 항목 발생 시 자동 실행되는 구조 |
| 워크플로우 흐름 설명 포함 | 충족 | Trigger → Filter → Action 1 → Action 2 흐름 설명 포함 |

---

## 7. 제약 사항 검토

### 7.1 구현 및 동작 제약

본 프로젝트는 설계 문서만 작성한 것이 아니라, Zapier에서 실제 워크플로우를 구성하였다.

구현된 구조는 다음과 같다.

```text
RSS 새 항목 발생
→ 제목에 "부동산" 포함 여부 필터링
→ Google Sheets 스프레드시트 생성
→ Google Sheets 행 추가
```

다만 현재 실행 결과 화면에서는 다음 메시지가 표시되었다.

```text
We couldn't find any new feeds.
```

따라서 최종 제출 시에는 RSS 피드에 새 항목이 발생했을 때 자동 실행된 결과 또는 테스트용 RSS 항목을 이용한 성공 캡처를 추가하는 것이 좋다.

---

### 7.2 보안 및 제출물 제약

제출 자료에서는 다음 사항을 주의해야 한다.

- API Key 노출 없음
- 토큰 노출 없음
- 비밀번호 노출 없음
- 계정 이메일 또는 개인 정보는 필요 시 일부 마스킹 처리
- Google Sheets 공유 링크 제출 시 접근 권한 확인 필요

예시:

```text
example***@gmail.com
API Key: ***
Token: ***
```

현재 제시된 이미지에서는 민감한 API Key나 토큰은 확인되지 않는다.

---

### 7.3 과금 리스크 검토

이미지 상단에 다음 안내가 표시되어 있다.

```text
This Zap uses paid features that are included in your free trial.
```

따라서 현재 Zap은 무료 체험 기간에는 실행 가능하지만, 체험 종료 후에는 유료 기능 사용으로 인해 계속 실행되지 않을 수 있다.

#### 과금 리스크

| 항목 | 내용 |
|---|---|
| 사용 도구 | Zapier |
| 과금 가능성 | 있음 |
| 원인 | Zapier의 일부 기능 또는 실행 조건이 유료 플랜에 포함될 수 있음 |
| 현재 상태 | Free trial 기간 내 사용 가능 |

#### 무료 대안

무료 플랜 중심으로 구현하려면 다음 대안을 고려할 수 있다.

1. **Make + Google Sheets**
   - Make 무료 플랜 범위 내에서 RSS 감지와 Google Sheets 저장 가능

2. **Google Apps Script**
   - Google Sheets와 RSS 파싱을 직접 연결 가능
   - 무료로 구현 가능하지만 코드 작성 필요

3. **Zapier 무료 기능만 사용**
   - 유료 기능이 포함된 단계가 있는지 확인 후, 무료 플랜에서 가능한 앱과 액션으로 단순화

---

## 8. 최종 평가

현재 이미지 기준으로 프로젝트 2 워크플로우는 다음 조건을 만족한다.

```text
Trigger 1개 이상 포함: 충족
Action 2개 이상 포함: 충족
Filter 1개 이상 포함: 충족
자동 실행 구조: 충족
반복 업무 정의: 충족
도구 선정 및 이유: 충족
```

다만 실행 결과 화면에서는 **신규 RSS 피드가 없어 실행 실패 메시지**가 표시되었으므로, 최종 제출 전에는 다음 중 하나를 추가로 확보하는 것이 좋다.

1. 새 RSS 항목이 실제로 발생한 뒤 자동 실행 성공 화면 캡처
2. Google Sheets에 행이 추가된 결과 화면 캡처
3. Zapier 실행 기록에서 성공 로그 캡처

---

## 9. 결론

본 프로젝트에서는 Zapier를 활용하여 **부동산 관련 RSS 글 자동 수집 워크플로우**를 구현하였다.

RSS 피드에 새 글이 등록되면 Zapier가 이를 감지하고, 제목에 **“부동산”** 키워드가 포함된 경우에만 Google Sheets로 데이터를 저장하도록 구성하였다.

구현된 워크플로우는 다음 요구사항을 대부분 충족한다.

- Trigger 1개 이상 포함
- Action 2개 이상 포함
- Filter 조건 포함
- 자동 실행 구조 구현
- 반복 업무 정의 및 도구 선정 이유 작성

단, 제출 완성도를 높이기 위해서는 **실제 Google Sheets에 데이터가 저장된 성공 결과 캡처**를 추가하는 것이 권장된다. 잘 구성하셨고, 이제 성공 실행 캡처만 확보하면 보고서 완성도가 더 높아질 것입니다.
