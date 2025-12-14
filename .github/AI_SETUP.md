# 🤖 AI 질문 생성 설정 가이드

PR이 생성되면 발표 내용을 기반으로 AI가 자동으로 질문을 생성합니다.

---

## 지원 AI Provider

| Provider | 서비스 | 모델 예시 |
|----------|--------|-----------|
| `openai` | OpenAI | gpt-4o, gpt-4-turbo, gpt-3.5-turbo |
| `anthropic` | Anthropic | claude-sonnet-4-20250514, claude-3-opus-20240229 |
| `google` | Google AI | gemini-1.5-pro, gemini-1.5-flash |
| `openai-compatible` | OpenAI 호환 API | Groq, Together AI, Ollama 등 |

---

## 설정 방법

### 1. GitHub Secrets 설정

Repository → Settings → Secrets and variables → Actions → New repository secret

### 2. 필수 Secret

| Secret Name | 설명 | 예시 |
|-------------|------|------|
| `AI_API_KEY` | AI 서비스 API 키 | `sk-xxxxx...` |

### 3. 선택 Secret

| Secret Name | 설명 | 기본값 |
|-------------|------|--------|
| `AI_PROVIDER` | AI 제공자 | `openai` |
| `AI_MODEL` | 사용할 모델 | Provider별 기본 모델 |
| `AI_BASE_URL` | 커스텀 API URL | Provider별 기본 URL |

---

## Provider별 설정 예시

### OpenAI

```
AI_API_KEY   = sk-xxxxxxxxxxxxxxxxxxxxxxxx
AI_PROVIDER  = openai
AI_MODEL     = gpt-4o  (선택)
```

### Anthropic (Claude)

```
AI_API_KEY   = sk-ant-xxxxxxxxxxxxxxxxxxxxxxxx
AI_PROVIDER  = anthropic
AI_MODEL     = claude-sonnet-4-20250514  (선택)
```

### Google (Gemini)

```
AI_API_KEY   = AIzaxxxxxxxxxxxxxxxxxxxxxxxx
AI_PROVIDER  = google
AI_MODEL     = gemini-1.5-flash  (선택)
```

### Groq (OpenAI 호환)

```
AI_API_KEY   = gsk_xxxxxxxxxxxxxxxxxxxxxxxx
AI_PROVIDER  = openai-compatible
AI_MODEL     = llama-3.1-70b-versatile
AI_BASE_URL  = https://api.groq.com/openai/v1/chat/completions
```

### Together AI (OpenAI 호환)

```
AI_API_KEY   = xxxxxxxxxxxxxxxxxxxxxxxx
AI_PROVIDER  = openai-compatible
AI_MODEL     = meta-llama/Meta-Llama-3.1-70B-Instruct-Turbo
AI_BASE_URL  = https://api.together.xyz/v1/chat/completions
```

### Local LLM - Ollama (OpenAI 호환)

```
AI_API_KEY   = ollama  (아무 값이나)
AI_PROVIDER  = openai-compatible
AI_MODEL     = llama3.1
AI_BASE_URL  = http://localhost:11434/v1/chat/completions
```

---

## 기본 모델

Secret에 `AI_MODEL`을 설정하지 않으면 아래 기본값이 사용됩니다:

| Provider | 기본 모델 |
|----------|-----------|
| openai | gpt-4o |
| anthropic | claude-sonnet-4-20250514 |
| google | gemini-1.5-flash |
| openai-compatible | gpt-4o |

---

## 동작 방식

1. PR 생성 시 `YYYY/weekNN-MM-DD/*/README.md` 파일 감지
2. 발표 내용 추출 (최대 4000자)
3. AI API 호출하여 질문 생성
4. PR에 자동으로 코멘트 작성

---

## 트러블슈팅

### API 키 오류

```
Error: Invalid API key
```
→ `AI_API_KEY` Secret이 올바르게 설정되었는지 확인

### 모델 없음 오류

```
Error: Model not found
```
→ `AI_MODEL` 값이 해당 Provider에서 지원하는 모델인지 확인

### Rate Limit 오류

```
Error: Rate limit exceeded
```
→ API 사용량 한도 초과. 잠시 후 다시 시도하거나 플랜 업그레이드

### OpenAI 호환 API 연결 실패

```
Error: Failed to fetch
```
→ `AI_BASE_URL`이 올바른지, 서비스가 실행 중인지 확인

---

## 비활성화 방법

AI 질문 생성을 사용하지 않으려면:

1. `AI_API_KEY` Secret을 삭제하거나
2. `.github/workflows/ai-questions.yml` 파일 삭제
