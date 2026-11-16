# 교양 트랙: 기술 판단을 위한 배경 지식

**깊이**: 개념 이해 + 논문 판단 (3단계 읽기 중 1~2회차)
**완료 기준(공통)**: 해당 분야 논문의 초록을 읽고 [6가지 질문](study-method.md#3-기술을-판단하는-6가지-질문)에 답할 수 있다
**시기**: 주력 트랙과 병행

> 문헌 목록의 `[ ]`는 "원문을 확인하고 읽었다"를 뜻합니다.

---

## L1. VR·XR 전반

이 트랙 전체의 기준서입니다. 디스플레이, 지각, 트래킹, 렌더링을 하나의 체계로 다룹니다.

- [ ] Steven LaValle, *Virtual Reality* (Cambridge University Press, 온라인 무료 공개): 수학적으로 정리된 VR 교재
- [ ] Jason Jerald, *The VR Book: Human-Centered Design for Virtual Reality* (2015): 사람 중심 설계 관점

## L2. 디스플레이·광학 기초

기초 지식이 없는 상태에서 시작하므로 **설계할 수준이 아니라 "트레이드오프를 설명할 수 있는 수준"**을 목표로 합니다.

**설명할 수 있어야 하는 것**: PPD와 인간 시력의 한계, FOV·eyebox·크기의 트레이드오프, Fresnel과 Pancake 렌즈의 차이, AR 도파관의 원리, VAC(초점 불일치)

- [ ] LaValle, *Virtual Reality*: 빛과 광학, 시각 생리 관련 장 (여기서 시작)
- [ ] David Hoffman et al., *Vergence–Accommodation Conflicts Hinder Visual Performance and Cause Visual Fatigue* (Journal of Vision, 2008)
- [ ] George Koulieris et al., *Near-Eye Display and Tracking Technologies for Virtual and Augmented Reality* (Eurographics STAR, 2019)
- [ ] Bernard Kress, *Optical Architectures for Augmented-, Virtual-, and Mixed-Reality Headsets* (SPIE Press, 2020): 더 깊이 가고 싶을 때

## L3. SLAM·트래킹

**설명할 수 있어야 하는 것**: SLAM 문제를 MAP 추정 → 최소제곱으로 정식화하는 과정, 필터 방식과 최적화 방식의 트레이드오프, 연구와 제품의 선택이 다른 이유

- [ ] Cesar Cadena et al., *Past, Present, and Future of Simultaneous Localization and Mapping* (IEEE T-RO, 2016): 분야 전체 서베이
- [ ] Georg Klein & David Murray, *Parallel Tracking and Mapping for Small AR Workspaces* (ISMAR 2007): PTAM
- [ ] Hauke Strasdat, J.M.M. Montiel, Andrew Davison, *Visual SLAM: Why Filter?* (Image and Vision Computing, 2012)
- [ ] Anastasios Mourikis & Stergios Roumeliotis, *A Multi-State Constraint Kalman Filter for Vision-aided Inertial Navigation* (ICRA 2007): MSCKF

## L4. Presence·Embodiment (몰입의 이론)

**설명할 수 있어야 하는 것**: Immersion과 Presence의 차이, Place Illusion과 Plausibility Illusion, Embodiment의 세 요소

- [ ] Mel Slater & Sylvia Wilbur, *A Framework for Immersive Virtual Environments (FIVE)* (Presence, 1997)
- [ ] Mel Slater, *Place Illusion and Plausibility Can Lead to Realistic Behaviour in Immersive Virtual Environments* (Phil. Trans. R. Soc. B, 2009)
- [ ] Konstantina Kilteni, Raphaela Groten, Mel Slater, *The Sense of Embodiment in Virtual Reality* (Presence, 2012)
- [ ] Matthew Botvinick & Jonathan Cohen, *Rubber Hands 'Feel' Touch That Eyes See* (Nature, 1998)
- [ ] Nick Yee & Jeremy Bailenson, *The Proteus Effect* (Human Communication Research, 2007)

## L5. 사이버 멀미

**설명할 수 있어야 하는 것**: 감각 충돌 이론과 자세 불안정 이론, SSQ 측정, 렌더링 지연·프레임 드랍과 멀미의 관계

- [ ] Robert Kennedy et al., *Simulator Sickness Questionnaire* (International Journal of Aviation Psychology, 1993)
- [ ] Gary Riccio & Thomas Stoffregen, *An Ecological Theory of Motion Sickness and Postural Instability* (Ecological Psychology, 1991)

## L6. AR 이론과 3D 상호작용

- [ ] Paul Milgram & Fumio Kishino, *A Taxonomy of Mixed Reality Visual Displays* (1994)
- [ ] Ronald Azuma, *A Survey of Augmented Reality* (Presence, 1997)
- [ ] Jannick Rolland & Henry Fuchs, *Optical Versus Video See-Through Head-Mounted Displays in Medical Visualization* (Presence, 2000)
- [ ] Doug Bowman et al., *3D User Interfaces: Theory and Practice*: 상호작용 교재
- [ ] Frank Steinicke et al., *Estimation of Detection Thresholds for Redirected Walking Techniques* (IEEE TVCG, 2010)
- [ ] Mahdi Azmandian et al., *Haptic Retargeting* (CHI 2016)

---

## 보류

지금은 하지 않고, 필요해지면 [docs/decisions/](../docs/decisions/)에 결정 기록을 남기고 트랙을 올립니다.

| 분야 | 보류 이유 | 다시 검토할 계기 |
|---|---|---|
| SLAM 직접 구현 심화 (Barfoot, Hartley & Zisserman, 리 군 최적화) | 주력이 렌더링이고, 교양 수준으로 판단력은 충분 | MR 합성·패스스루 렌더링을 깊게 다루게 될 때 |
| 광학 설계 | 기초 지식이 없고, 렌더링 판단에는 교양 수준이면 충분 | 디스플레이 쪽 진로에 관심이 생길 때 |
| 지각 실험 연구 (실험 설계, 통계 모형) | 직접 실험을 할 계획이 없음 | Foveation 품질 기준을 직접 측정하고 싶을 때 |
