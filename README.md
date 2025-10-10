# blog9yu-content

blog9yu.dev 블로그의 컨텐츠 저장소입니다.

## 폴더 구조

```
blog9yu-content/
├── posts/                                  # 블로그 포스트 (포스트별 폴더)
│   ├── janus-gateway/
│   │   ├── index.mdx                      # 포스트 내용
│   │   └── images/                        # 포스트 전용 이미지
│   │       └── janus-gateway-01.png
│   ├── react-performance-optimization/
│   │   ├── index.mdx
│   │   └── images/
│   └── nextjs-15-whats-new/
│       ├── index.mdx
│       └── images/
└── README.md
```

## Frontmatter 스키마

모든 MDX 파일은 다음 형식의 Frontmatter를 포함해야 합니다:

```yaml
---
# 필수 필드
title: "포스트 제목"
description: "포스트 요약 (1-2문장)"
slug: "post-slug" # 폴더명과 동일해야 함
date: "2025-10-06T00:00:00.000Z" # ISO 8601 형식
private: false

# 선택 필드
tags: ["React", "TypeScript", "Next.js"] # 빈 배열 가능
thumbnail: "./images/cover.png" # 상대 경로, 없으면 null
series: "시리즈명" # 없으면 null
seriesOrder: 1 # 시리즈 내 순서, 없으면 null
---
```

## 작성 규칙

1. **폴더명 = slug**: 폴더명과 `slug` 필드는 반드시 일치해야 합니다.
   - 예: `posts/nextjs-optimization/` → `slug: "nextjs-optimization"`

2. **파일명**: 항상 `index.mdx` 사용

3. **날짜 형식**: `date`는 ISO 8601 형식 사용
   - 예: `"2025-10-06T00:00:00.000Z"`

4. **태그**: 선택 필드로 빈 배열도 가능, PascalCase 권장
   - 예: `["React", "Next.js", "WebRTC"]` 또는 `[]`

5. **시리즈**: 동일한 시리즈명으로 그룹화, `seriesOrder`로 순서 지정
   - 예: `series: "React 완벽 가이드"`, `seriesOrder: 1`
   - 시리즈가 없으면 `series: null`, `seriesOrder: null`

6. **Null 명시**: 선택 필드에 값이 없으면 `null`로 명시
   - 예: `thumbnail: null`, `series: null`, `seriesOrder: null`

## 이미지 관리

- 이미지는 각 포스트 폴더 내 `images/` 하위 폴더에 저장
- **상대 경로** 사용 권장

  ```yaml
  # Frontmatter
  thumbnail: "./images/cover.png"
  ```

  ```markdown
  # MDX 본문

  ![설명](./images/screenshot.png)
  ```

- 외부 URL도 지원
  ```yaml
  thumbnail: "https://example.com/image.png"
  ```

## 검증

모든 포스트는 빌드 타임에 Zod 스키마로 검증됩니다.

- Frontmatter 필수 필드 누락 시 빌드 실패
- url_slug 불일치 시 경고
- 시리즈 index 중복 시 에러
