# 주력 트랙: 실시간 렌더링

**깊이**: 수식 유도 + 이해 확인용 구현
**완료 기준(공통)**: 각 단계의 "이해 확인" 질문에 노트 없이 답하고 유도할 수 있다

> 문헌 목록의 `[ ]`는 "원문을 확인하고 읽었다"를 뜻합니다. 서지 정보는 읽기 전에 원문으로 확인하세요.

---

## 0단계. 수학 기반

렌더링의 모든 단계가 이 수학 위에 있습니다.

**핵심 주제**
- 벡터 공간, 기저, 선형 변환으로서의 행렬
- 기저 변환과 좌표계 (Local → World → View → Clip → NDC → Screen)
- 동차 좌표(homogeneous coordinates)와 아핀 변환
- 사영 변환과 원근 분할(perspective divide)
- 회전 표현: 회전 행렬, 오일러 각, 쿼터니언, 축-각
- 법선 벡터 변환 (역전치 행렬)

**문헌**
- [ ] Gilbert Strang, *Introduction to Linear Algebra*: 선형대수의 정석
- [ ] 3Blue1Brown, *Essence of Linear Algebra* (영상 시리즈): 기하학적 직관
- [ ] Fletcher Dunn & Ian Parberry, *3D Math Primer for Graphics and Game Development*: 게임·그래픽스 관점의 3D 수학
- [ ] Eric Lengyel, *Foundations of Game Engine Development, Vol. 1: Mathematics*: 더 엄밀한 엔진 수학

**이해 확인**
- 법선 벡터를 변환할 때 왜 모델 행렬이 아니라 **역전치 행렬**을 써야 하는가? 유도하라
- 원근 투영 행렬을 직접 유도하라. 왜 깊이 값이 비선형으로 저장되는가?
- 쿼터니언 회전 `q v q*`가 왜 회전이 되는가?

---

## 1단계. 래스터화 파이프라인

삼각형이 화면의 픽셀이 되기까지의 과정을 수학으로 이해합니다.

**핵심 주제**
- 정점 변환과 클리핑 (동차 좌표계에서의 클리핑)
- Edge function과 무게중심 좌표(barycentric coordinates)
- **원근 보정 보간** (왜 `1/w`로 보간해야 하는가)
- Z-버퍼와 깊이 정밀도 (Reversed-Z가 왜 정밀도를 개선하는가)
- 텍스처 좌표와 텍스처 샘플링

**문헌**
- [ ] Steve Marschner & Peter Shirley, *Fundamentals of Computer Graphics*: 래스터화·시점 변환 장
- [ ] Juan Pineda, *A Parallel Algorithm for Polygon Rasterization* (SIGGRAPH 1988): Edge function 래스터화의 원조
- [ ] Fabian Giesen, *A Trip Through the Graphics Pipeline* (블로그 시리즈, 2011): 실제 GPU가 파이프라인을 처리하는 방식

**이해 확인 구현**: `SoftRasterizer` 저장소 (CPU만으로 텍스처 입힌 3D 모델 렌더링)

**이해 확인**
- 화면 공간에서 무게중심 좌표로 선형 보간하면 텍스처가 왜 휘어 보이는가? 올바른 식을 유도하라
- Near plane을 너무 가깝게 두면 Z-fighting이 왜 심해지는가?

---

## 2단계. 샘플링과 신호처리

계단 현상(앨리어싱)은 왜 생기고, 왜 TAA·업스케일링 같은 기법이 필요한가를 이해합니다.

**핵심 주제**
- 샘플링 정리(나이퀴스트)와 앨리어싱
- 푸리에 변환의 직관, 필터와 재구성
- 밉맵과 텍스처 필터링 (이중선형, 삼선형, 비등방성)
- 슈퍼샘플링과 MSAA

**문헌**
- [ ] Matt Pharr, Wenzel Jakob, Greg Humphreys, *Physically Based Rendering* (4판, 온라인 무료 공개): 샘플링과 재구성 장
- [ ] Lance Williams, *Pyramidal Parametrics* (SIGGRAPH 1983): 밉맵의 원조

**이해 확인**
- 체크무늬 바닥이 멀리서 물결무늬(모아레)로 보이는 이유를 샘플링 정리로 설명하라
- 밉맵 레벨은 어떤 식으로 선택되는가?

---

## 3단계. 셰이딩과 빛의 물리

"물체가 왜 그렇게 보이는가"를 물리와 확률로 이해합니다. PBR(물리 기반 렌더링)의 기반입니다.

**핵심 주제**
- 복사측정학(radiometry): radiance, irradiance, solid angle
- 렌더링 방정식
- BRDF와 에너지 보존, 마이크로패싯 이론 (GGX 분포)
- 몬테카를로 적분과 중요도 샘플링
- 실시간 근사: Split-sum 근사, 이미지 기반 조명(IBL)

**문헌**
- [ ] James Kajiya, *The Rendering Equation* (SIGGRAPH 1986)
- [ ] Robert Cook & Kenneth Torrance, *A Reflectance Model for Computer Graphics* (1982)
- [ ] Bruce Walter et al., *Microfacet Models for Refraction through Rough Surfaces* (EGSR 2007): GGX 분포
- [ ] Brent Burley, *Physically-Based Shading at Disney* (SIGGRAPH 2012 코스)
- [ ] Brian Karis, *Real Shading in Unreal Engine 4* (SIGGRAPH 2013 코스): UE4·UE5 셰이딩 모델의 기반
- [ ] Tomas Akenine-Möller et al., *Real-Time Rendering* (4판): 물리 기반 셰이딩 장
- [ ] Joseph Blitzstein & Jessica Hwang, *Introduction to Probability*: 몬테카를로에 필요한 확률 기초

**이해 확인**
- 렌더링 방정식의 각 항이 물리적으로 무엇을 뜻하는가?
- BRDF가 에너지 보존을 만족하려면 어떤 조건이 필요한가?
- 중요도 샘플링은 왜 분산을 줄이는가?

---

## 4단계. 실시간 렌더링 기법

AAA 게임에서 실제로 쓰는 기법과 그 트레이드오프를 이해합니다.

**핵심 주제**
- Forward vs Deferred 렌더링 (VR이 Forward를 선호하는 이유 포함)
- 그림자 맵과 그 문제들 (앨리어싱, 바이어스, Cascaded Shadow Maps)
- **TAA**: 이전 프레임 재투영, 모션 벡터, 히스토리 거부(rejection)
- 업스케일링과 프레임 생성의 원리
- GPU 구조와 성능 (병렬 처리 모델, 대역폭, 오버드로우)

**문헌**
- [ ] Lance Williams, *Casting Curved Shadows on Curved Surfaces* (SIGGRAPH 1978): 그림자 맵의 원조
- [ ] Takafumi Saito & Tokiichiro Takahashi, *Comprehensible Rendering of 3-D Shapes* (SIGGRAPH 1990): G-buffer의 기원
- [ ] Brian Karis, *High Quality Temporal Supersampling* (SIGGRAPH 2014 코스): UE4 TAA
- [ ] Lei Yang, Shiqiu Liu, Marco Salvi, *A Survey of Temporal Antialiasing Techniques* (Computer Graphics Forum, 2020)
- [ ] *Real-Time Rendering* (4판): 그림자, 안티앨리어싱 장

**이해 확인**
- TAA의 재투영 식을 쓰고, 고스팅(ghosting)이 왜 생기는지 설명하라
- Deferred 렌더링에서 MSAA가 왜 어려운가?

---

## 5단계. XR 렌더링

원래 목표인 XR 몰입 기술의 렌더링 부분입니다. **연결 트랙 B1~B3을 먼저 공부합니다.**

**핵심 주제**
- 스테레오 렌더링과 눈마다 다른 비대칭 절두체(off-axis projection)
- 렌즈 왜곡 보정과 색수차 보정
- **재투영**: 회전 Timewarp(`p' = K·R·K⁻¹·p`), 이동 보정과 disocclusion 문제
- Foveated rendering: 고정 방식, 시선 추적 방식, 주변시야 품질 기준
- 지연 예산: motion-to-photon 지연의 구성 요소

**문헌**
- [ ] Brian Guenter et al., *Foveated 3D Graphics* (SIGGRAPH Asia 2012)
- [ ] Anjul Patney et al., *Towards Foveated Rendering for Gaze-Tracked Virtual Reality* (SIGGRAPH Asia 2016)
- [ ] J.M.P. van Waveren, *The Asynchronous Time Warp for Virtual Reality on Consumer Hardware* (VRST 2016)
- [ ] Steven LaValle, *Virtual Reality* (온라인 무료 공개): 렌더링 관련 장

**이해 확인**
- 순수 회전일 때 재투영이 왜 호모그래피 하나로 정확하게 표현되는가? 이동이 있으면 왜 안 되는가?
- 시선 추적의 지연이 길면 Foveated rendering에서 어떤 문제가 보이는가?

---

## 6단계. 뉴럴 렌더링과 최신 기법

기술 판단력 연습의 주 무대입니다. 논문을 6가지 질문으로 분석합니다.

**핵심 주제**
- 미분 가능 렌더링과 최적화
- NeRF: 신경망으로 장면을 표현
- 3D Gaussian Splatting: 미분 가능한 래스터화로 장면을 표현
- XR에서의 적용과 한계 (모바일 성능, 움직이는 장면)

**문헌**
- [ ] Ben Mildenhall et al., *NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis* (ECCV 2020)
- [ ] Bernhard Kerbl et al., *3D Gaussian Splatting for Real-Time Radiance Field Rendering* (SIGGRAPH 2023)
- [ ] Ayush Tewari et al., *Advances in Neural Rendering* (Eurographics STAR, 2022)

**이해 확인**
- 3DGS는 NeRF의 어떤 문제를 해결했고, 무엇을 대가로 치렀는가?

---

## 선택: UE5 렌더링 (취업 연결)

이 저장소의 주 목표는 아니지만, 취업 포트폴리오와 연결할 때 참고합니다.

- UE5 렌더러 구조 (Render Dependency Graph), 커스텀 셰이더
- 3·4단계의 Karis 코스 노트가 UE 셰이딩·TAA의 기반이므로 자연스럽게 연결된다
