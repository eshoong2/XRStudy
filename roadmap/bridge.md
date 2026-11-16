# 연결 트랙: XR 렌더링에 필요한 다른 분야

**깊이**: 렌더링(주력 5단계)에 필요한 만큼 수식까지
**시기**: 주력 4단계를 마친 뒤, 5단계 전에

> 문헌 목록의 `[ ]`는 "원문을 확인하고 읽었다"를 뜻합니다.

---

## B1. 칼만 필터와 머리 자세 예측

**왜 필요한가**: 렌더링이 끝나 화면에 표시될 때쯤 머리는 이미 움직여 있습니다. 그래서 "몇 ms 뒤 머리가 어디 있을지" **예측한 자세**로 렌더링하고 재투영합니다.

**핵심 주제**
- 가우시안 분포, 베이즈 정리, 조건부 확률
- 선형 칼만 필터: 예측과 갱신, 공분산의 의미
- 확장 칼만 필터(EKF)와 비선형 모델
- 쿼터니언 운동학: 각속도로 회전을 적분하기
- IMU(자이로·가속도계) 노이즈 모델

**문헌**
- [ ] Greg Welch & Gary Bishop, *An Introduction to the Kalman Filter* (UNC 기술 보고서): 가장 짧은 입문
- [ ] Sebastian Thrun, Wolfram Burgard, Dieter Fox, *Probabilistic Robotics*: 가우시안 필터 장
- [ ] Joan Solà, *Quaternion Kinematics for the Error-State Kalman Filter* (arXiv 2017): 쿼터니언과 필터를 함께
- [ ] Steven LaValle et al., *Head Tracking for the Oculus Rift* (ICRA 2014): 실제 VR 헤드셋의 자세 추정과 예측

**이해 확인**
- 칼만 이득(Kalman gain)이 "어느 정보를 더 믿을지"를 어떻게 정하는가?
- 1차원 칼만 갱신식과 Ernst & Banks의 감각 통합 식이 같은 형태임을 보여라

---

## B2. 시선 추적의 원리

**왜 필요한가**: 시선 추적 기반 Foveated rendering은 "사용자가 어디를 보는가"를 알아야 합니다. 시선 추적의 정확도와 지연이 렌더링 품질을 좌우합니다.

**핵심 주제**
- 눈의 구조와 안구 운동 (fixation, saccade, smooth pursuit)
- 동공·각막 반사 기반 시선 추정의 기하학
- 시선 추적의 오차와 지연이 렌더링에 주는 영향

**문헌**
- [ ] Dan Witzner Hansen & Qiang Ji, *In the Eye of the Beholder: A Survey of Models for Eyes and Gaze* (IEEE TPAMI, 2010)
- [ ] George Koulieris et al., *Near-Eye Display and Tracking Technologies for Virtual and Augmented Reality* (Eurographics STAR, 2019): 시선 추적 부분

**이해 확인**
- 사카드(빠른 안구 운동) 중에 Foveated rendering의 품질을 낮춰도 되는 이유는 무엇인가?

---

## B3. 주변시야 지각과 정신물리학

**왜 필요한가**: "주변부 화질을 얼마나 낮춰도 사람이 눈치채지 못하는가"가 Foveated rendering의 품질 기준입니다. 이것을 측정하는 방법이 정신물리학입니다.

**핵심 주제**
- 이심률(eccentricity)에 따른 시력 저하
- 주변시야의 대비 민감도와 움직임 민감도
- 정신물리 측정: 심리측정 함수(psychometric function), 임계값, JND
- 감각 통합의 최적 추정 모델

**문헌**
- [ ] Hans Strasburger, Ingo Rentschler, Martin Jüttner, *Peripheral Vision and Pattern Recognition: A Review* (Journal of Vision, 2011)
- [ ] Felix Wichmann & N. Jeremy Hill, *The Psychometric Function: I. Fitting, Sampling, and Goodness of Fit* (Perception & Psychophysics, 2001)
- [ ] Marc Ernst & Martin Banks, *Humans Integrate Visual and Haptic Information in a Statistically Optimal Fashion* (Nature, 2002)

**이해 확인**
- 심리측정 함수를 실험 데이터에 피팅해서 임계값을 구하는 과정을 설명하라
- Patney et al. (2016)이 주변부에서 "대비"를 보존하려 한 이유는 무엇인가?
