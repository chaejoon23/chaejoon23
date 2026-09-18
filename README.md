## 채준 (JUN)

모든 것이 빠르게 바뀌고 편리해지는 시대 속에서, 저는 굳이 시간이 오래 걸리는 필름으로 세상을 기록하곤 합니다. 
그 대상을 바라보며 숨을 죽이던 나의 머뭇거림, 현장의 서늘한 공기와 그때 느꼈던 찰나의 감정까지 온전히 그 안에 남겨두고 싶기 때문입니다.

빠른 효율과 정교함만을 좇는 세상에서, 인공지능과 이미지 처리 기술 또한 점차 '가장 완벽한 결과물'만을 향해 달려가는 듯합니다. 
하지만 저는 차가운 수치와 픽셀 너머에 존재하는 인간의 시선과 감성의 온도를 기술에 담아내고 싶습니다.
감정을 차가운 기술로 대체하는 것이 아니라, 기술을 통해 인간 본연의 감각을 더욱 깊이 이해하고 이어주는 도구를 디자인하는 것. 

이것이 제가 대학원에 진학하여 탐구하고 싶은 것입니다.

---

### 지금 하는 것

#### 🎞 [Bin_pind](https://github.com/chaejoon23/Bin_pind) — 화질·ISP
비정형 비디오 스트림에서 시공간적 POI(Point of Interest)를 추출해 Georeferencing하는 파이프라인. 
핵심 병목은 VLM(Vision-Language Model) 추론 직전의 프런트엔드 비전 프로세싱이었습니다. 균일 샘플링(1 fps) 프레임을 VLM의 토크나이저로 직접 전달할 경우 
발생하는 연산 오버헤드와 정보 중복도를 완화하기 위해, DINO 기반 피처 맵 임베딩 간 코사인 유사도를 측정하여 중복 프레임을 제거했습니다. 
또한 극한의 저조도 환경에서 텍스트 토큰 인식률이 급락하는 문제를 해결하고자 sRGB 경량 ISP 파이프라인을 구축했습니다.

Shades-of-Gray 기반 오토 화이트밸런스 → 로컬 통계 기반 적응형 감마 보정 → 노이즈 표준편차 추정 기반의 조건부 NL-Means → LAB 색공간 CLAHE → 에지 인지형 언샤프 마스킹.
텍스트 영역의 Saliency map과 MSER 기반 문자 검출을 결합하여 VLM에 입력될 최적의 대표 프레임을 선별합니다.

> 저조도 복원을 화질 게이트보다 **앞에** 둬야 한다는 걸 프레임을 잃어보고 알았습니다.
> 순서를 반대로 두면 실내에서 방문한 장소가 "품질 미달"로 통째로 사라집니다.
> → [설계 근거와 실패했던 시도들](https://github.com/chaejoon23/Bin_pind/blob/main/docs/vision-frontend.md)

#### 🔍 [dinov3-image-search](https://github.com/chaejoon23/dinov3-image-search) — 표현학습
단일 쿼리 이미지 기반 Visual Place Recognition(VPR). DINOv3의 Self-Supervised Learning 패치 토큰 및 CLS 토큰에서 384차원의 Representation을 추출해 코사인 유사도 기반의 임베딩 공간 검색을 수행합니다. 도심 거리 시퀀스의 GPS 메타데이터·타임스탬프·헤딩 벡터와 결합하여, 표현 공간 내 k-NN탐색을 6-DoF 위치 추정 파이프라인으로 매핑했습니다.
> 처음 구현에서 사전학습 가중치를 로드하지 않고 있었는데도 데모가 "돌아가는 것처럼"
> 보였습니다. 랜덤 초기화 ViT도 저수준 구조는 보존하기 때문입니다. 무작위 기대값을
> 기준선으로 깔고 Precision@k를 재서 확인했습니다.

#### 📱 [autofoto](https://github.com/chaejoon23/autofoto) — 온디바이스 배포
엣지 디바이스 환경에서의 실시간 시각 인식 추론 파이프라인. 프라이버시 보존 및 추론 지연시간(Latency) 최소화를 위해 서버 오프로딩 없이 디바이스 온칩 NPU/GPU 가속을 타겟팅했습니다. 런타임 모델 레지스트리를 분리하여 동적 아티팩트 페칭 구조를 설계했으며, 클라이언트 재빌드 없이 경량 백본의 가중치를 무중단 배포 및 교체할 수 있도록 모듈화했습니다.
Flutter · TensorFlow Lite · MobileNetV2.

---

### 해온 것

| | |
|---|---|
| **연구실** | 백석대학교 IPCG 연구실 (지도교수 곽노윤) — 2025.04 ~ 현재<br>매주 교재 세미나·발표. 『케라스 창시자에게 배우는 딥러닝』(F. Chollet) **2회독** → 2026.06부터 『딥러닝 파이토치 교과서』(서지영) |
| **논문** | 「한국어 형태소 정규화와 복잡도 기반의 라우팅을 이용한 품질 검증형 LLM API 비용 최적화 프록시」<br>한국디지털콘텐츠학회 2026 하계종합학술대회 대학생논문경진대회 **은상** · 제1저자 → [논문 · 실험 하네스 · 대시보드](https://github.com/chaejoon23/minT) |
| **특허** | 「영상 콘텐츠 기반의 여행 정보 제공 방법 및 시스템」 (출원) |
| **수상·선정** | 백석대 창업경진대회 대상 · 충남 RISE 대학 연합 창업경진대회 최우수상<br>모두의 창업 프로젝트 1기 **1차 1라운드 통과** — 창업활동자금 200만원 (Pind) |
| **개발** | BoothUP — 팝업 참가기업 모집 B2B 플랫폼 메인 개발자 (운영 중)<br>로보틱스·자율주행 교육 콘텐츠, 딥러닝 강의자료 제작 |

다루어 온 도메인은 언어와 비전으로 확장되어 왔으나 본질적인 연구 질문은 일관됩니다 — Resource-constrained Environment에서의 최적 추론 효율성 확보.
제한된 컴퓨팅 예산 하에서 추론 경로를 결정하는 Dynamic Routing을 탐구했고, 현재는 비전 트랜스포머의 계산 복잡도를 낮추기 위한 Token Pruning과 엣지향 ISP 통합 경량화 연구로 그 궤적을 넓혀가고 있습니다.

---

### 쓰는 것

**비전·AI** OpenCV · NumPy · PyTorch · TensorFlow Lite · DINOv3 · Gemini · faster-whisper
**백엔드** FastAPI · SQLAlchemy 2.0 · PostgreSQL + PostGIS · Supabase
**프론트·앱** TypeScript · Next.js · React · Flutter
**품질** ruff(ANN) · mypy strict · pytest · pre-commit

📫 chaejoon23@gmail.com
