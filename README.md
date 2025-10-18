# 🎥 AI Video Content Analyzer

# AI Video Analyzer 실행 전용 구성 설치 및 실행 매뉴얼

이 문서는 Docker 환경에서 **AI Video Analyzer**를 설치하고 실행하는 방법을 안내합니다.

---

## 1. 요구사항

- Docker >= 24
- docker-compose >= 2.10
- GPU 사용 권장 (CUDA 지원), CPU도 가능하지만 속도 저하
- 최소 24GB 이상 VRAM 권장

---

## 2. 파일 및 경로 구성

```bash
video-analyzer/ # 사용자가 경로 임의 설정 가능 (workspace 등, github clone 한 디렉토리 또는 zip 파일 압축해제한 디렉토리)
├─ docker-compose.yml # 도커 컴포즈 설정 파일
├─ docker-up.cmd # 최초 1회 실행 명령. 컨테이너 이미지 다운로드, 분석 모델 다운로드 및 gradio 실행
├─ tail-logs.cmd # 컨테이너 이미지 내부 로그 확인
├─ docker-stop.cmd # 컨테이너 서비스 중지
├─ docker-start.cmd # 중단 된 컨테이너 다시 시작
├─ docker-down.cmd # 컨테이너 서비스 중지 후 이미지 언로드 (컨테이너 이미지 파일은 남아 있음)
├─ models/ # 자동생성: Vision Language 모델 캐시/다운로드 폴더
├─ videos/ # 자동생성: 업로드 된 비디오 저장 폴더
├─ outputs/ # 자동생성: 영상 분석 결과 텍스트 파일 저장 폴더
└─ README.md # 애플리케이션 설치 안내 파일

> `models`, `videos`, `outputs` 폴더는 호스트와 컨테이너 간 공유되는 디렉토리로, 자동으로 연동(볼륨 마운트)됩니다.

```

## 3. 최초 컨테이너 이미지 다운로드 및 자동 실행

```cmd
docker-up.cmd
# docker-compose.yml의 제일 하단, command: ["python", "run-gradio.py", "--share"] 로 바꾸고, docker-down.cmd > docker-up.cmd 실행하면 gradio를 외부 공개모드인 live 모드로 실행
```
기본 포트: 7860

- Gradio UI 접속: http://localhost:7860

## 4. 프로프램 중지
```
docker-stop.cmd
```

## 5. 프로프램 재시작
```
docker-start.cmd
```

## 6. 컨테이너 이미지 로그 확인
```
tail-logs.cmd
```

## 7. 컨테이너 완전히 셧다운 및 이미지 언로드
```
docker-down.cmd
```

## 8. 디스크 및 환경 변수

| 호스트 폴더   | 컨테이너 경로                         | 설명      |
| ----------- |-------------------------------------|-----------|
| `./models`  | `/workspace/video_analyzer/models`  | Vision Language 모델 다운로드/저장 |
| `./videos`  | `/workspace/video_analyzer/videos`  | 업로드 된 영상 |
| `./outputs` | `/workspace/video_analyzer/outputs` | 분석된 텍스트 |

### 환경 변수
- CUDA_VISIBLE_DEVICES=0 : GPU 선택
- HF_HOME, TRANSFORMERS_CACHE, HF_HUB_CACHE : 모델 캐시 경로

## 9. 사용 방법
#### 1. 브라우저에서 Gradio 웹 UI 접속 (http://localhost:7860)
#### 2. 비디오 업로드
#### 3. 필요시 System Settings에 있는 System Prompt, Max Tokens, FPS 등 조정
#### 4. 🚀 영상 분석 클릭
#### 5. 분석 완료 후 화면에 결과 출력되며, outputs 폴더에도 .txt 파일이 저장됨
#### - 분석 텍스트 파일명은 업로드한 영상 파일명과 동일하며, 중복 파일명을 방지하기 위해 영상과 텍스트 파일명 끝에 임의의 난수 문자열이 추가 됩니다.

## 10. 주의 사항
- 긴 영상(1분 이상) 사용 시 VRAM 부족 가능
- FPS, Max Tokens 조절로 GPU 메모리 사용 최적화 가능
- Docker 환경에서는 /workspace/video_analyzer 경로 기준으로 볼륨이 마운트되어야 정상 동작

## 11. 📌 서비스 제공 전문가 연락처
```
이메일 : ex.friend.ai@gmail.com 또는 methodtweak@naver.com
전화번호 : 010-8865-7020
```

