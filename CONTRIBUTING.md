# 🤿 Contributing Guide

Fathom 스터디에 참여하는 방법을 안내합니다.

---

## 📝 발표자료 올리는 법

### 1. 브랜치 생성

```bash
git checkout main
git pull origin main
git checkout -b feat/week51-홍길동-spring-batch
```

### 2. 폴더 구조 생성

```
2025/week51-12-16/홍길동-spring-batch/
├── README.md      # 발표 내용
├── slides.pdf     # 슬라이드
└── QnA.md         # Q&A (발표 후 작성)
```

### 3. 템플릿 복사

```bash
cp templates/presentation.md 2025/week51-12-16/홍길동-spring-batch/README.md
cp templates/qna.md 2025/week51-12-16/홍길동-spring-batch/QnA.md
```

### 4. 커밋 &amp; 푸시

```bash
git add .
git commit -m "[week51] 홍길동 - Spring Batch 발표자료 추가"
git push origin feat/week51-홍길동-spring-batch
```

### 5. PR 생성

- PR 템플릿에 맞춰 작성
- 월요일 자정까지 생성
- 리뷰어: 다른 팀원 1명 이상

---

## 📏 마크다운 작성 가이드

### 권장 구조

```markdown
# 제목

## 개요
왜 이 주제를 선택했는지

## 본문
### 섹션 1
### 섹션 2
### 섹션 3

## 실습 / 데모
코드나 예제

## 결론
핵심 요약

## References
참고 자료 링크
```

### 코드 블록

언어 명시 필수:

```java
public class Example {
    // ...
}
```

### 이미지

`images/` 폴더에 저장 후 상대 경로로:

```markdown
![설명](./images/diagram.png)
```

---

## 🏷️ 커밋 컨벤션

```
[weekNN] 이름 - 설명

예시:
[week51] 홍길동 - Spring Batch 발표자료 추가
[week51] 홍길동 - Q&A 정리
[week51] 홍길동 - 피드백 반영
```

---

## ❓ Q&A 작성법

발표 후 3일 이내에 `QnA.md` 작성:

1. 오프라인에서 받은 질문
2. AI가 생성한 질문 (gemini 활용)
3. 본인이 추가로 고민한 질문

답변은 최대한 상세하게!
