---
title: "폴리스너츠 한글판 패치 — 다운로드 · 적용법"
date: 2026-06-16
categories: ["폴리스너츠 한글화"]
tags: ["폴리스너츠", "한글패치", "세가새턴", "xdelta"]
---

## 다운로드

최신 패치는 GitHub **Releases** 에서 받으세요.

> 📦 [**최신 패치 다운로드 (Releases)**](https://github.com/) <!-- 배포 저장소 Releases 주소로 변경 -->

배포본 구성:

```
patch/   policenauts_kr_disc1~3.xdelta
cue/     Policenauts_KR (Disc 1~3).cue
README.txt
```

---

## 0. 먼저 — 이 패치가 요구하는 원본(정본)

**Redump 규격 BIN/CUE** (디스크별 2트랙)이 필요합니다.

| 파일 | 용도 |
|---|---|
| `Policenauts (Japan) (Disc N) (Track 1).bin` | 데이터 트랙 — **이 파일에 패치** |
| `Policenauts (Japan) (Disc N) (Track 2).bin` | 오디오 트랙 — 그대로 사용 |
| `Policenauts (Japan) (Disc N).cue` | 트랙 구성표 |

패치는 **딱 이 덤프에만** 적용됩니다. xdelta 는 원본 체크섬을 내장하므로,
다른 덤프에 적용하려 하면 `source checksum mismatch` 오류를 내고 **안전하게 멈춥니다**.

**패치 전, 본인 원본 Track 1 의 SHA-1 을 먼저 확인하세요:**

```bat
certutil -hashfile "Policenauts (Japan) (Disc 1) (Track 1).bin" SHA1
```

이 값이 [검증값](#검증값) 의 "원본 Track1 SHA-1" 과 같아야 합니다.

---

## 1. 다른 포맷을 가지고 있다면 → 먼저 정본(2트랙 BIN/CUE)으로 변환

- **CHD** (새턴 에뮬에서 가장 흔함)
  ```bat
  chdman extractcd -i 입력.chd -o "Policenauts (Japan) (Disc N).cue" -ob "Policenauts (Japan) (Disc N) (Track 1).bin"
  ```
  → 트랙별 bin/cue 로 풀린 뒤 Track 1 SHA-1 이 일치하면 OK.
- **단일 병합 .bin / .iso** — 트랙 경계로 다시 분할해야 합니다. 보통 같은 Redump 덤프를 다시 받는 게 빠릅니다.
- **MODE1/2048 덤프** — 이 패치는 MODE1/2352(원시 섹터) 기준입니다. 2352 덤프가 필요합니다.

> 변환 후 Track 1 SHA-1 이 일치하면 진행, 다르면 그 덤프는 대상이 아닙니다(다른 리비전/리덤프).

---

## 2. 패치 적용 (디스크 1·2·3 각각 반복)

### 방법 A) Delta Patcher (GUI, 가장 쉬움)
1. xdelta UI(Delta Patcher) 실행
2. **Patch**: `patch/policenauts_kr_disc{N}.xdelta`
   **Original**: 원본 `...(Disc N) (Track 1).bin`
3. **Apply Patch** → `Policenauts_KR (Disc N) (Track 1).bin` 생성

### 방법 B) xdelta3 (명령줄)
```bat
xdelta3 -d -s "Policenauts (Japan) (Disc N) (Track 1).bin" policenauts_kr_disc{N}.xdelta "Policenauts_KR (Disc N) (Track 1).bin"
```

---

## 3. 부팅용 구성

아래 3개를 같은 폴더에 두고 `.cue` 를 에뮬레이터로 엽니다.

| 파일 | 출처 |
|---|---|
| `Policenauts_KR (Disc N) (Track 1).bin` | 패치로 생성한 데이터 트랙 |
| `Policenauts (Japan) (Disc N) (Track 2).bin` | 원본 오디오 트랙 그대로 복사 |
| `Policenauts_KR (Disc N).cue` | 동봉 (cue/ 폴더) |

**권장 에뮬레이터: [Ymir](https://github.com/StrikerX3/Ymir)** (런타임 검증 완료).
실기(실제 새턴)는 EDC/ECC 재계산이 필요합니다.

---

## 검증값

> Release 의 `README.txt` 에 디스크별 원본/한글 Track1·원본 Track2 SHA-1 과 패치 크기가 들어 있습니다.
> 적용 후 산출물 Track1 SHA-1 을 대조하면 정상 패치를 확인할 수 있습니다.
