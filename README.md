# POSE Estimation Framework in VSLAM 

## Project Description

To train our deep learning system, we need ground truth information. We require a VSLAM (Visual Simultaneous Localization and Mapping) framework that can accurately estimate POSEs in various environments.

We want a clean, modular architecture VSLAM framework that allows us to use various algorithms as desired and conduct experiments to obtain accurate poses. Real-time computation is not a constraint.

## Roles

- 매니저 m:이세라
- 영상처리 m:안현석, s:서영훈
- 백엔드 m:형승호, s:안현석
- 프론트 m:서영훈, s:이세라
- 아키텍트 m:이세라, s:형승호, 서영훈
![Roles](https://www.mathworks.com/discovery/slam/_jcr_content/mainParsys3/discoverysubsection_158176500/mainParsys3/image.adapt.full.medium.png/1661234198941.png)
## Specs

- Ubuntu 18.04
- ROS melodic
- OpenCV 3.2
- Python
- C++ 14
- Eigen3

## To-do
- GUI 유틸리티 추가(?)

## Meeting Log
- 03/08
  - CI/CD
    1. 빌드 가능 여부(기본)
    2. CLI 아규먼트 별로 Git Action 만들어놓기
  - 성능지표 중 Xycar 환경 추가 (리얼센스까지는 필요없음)
    다음주 월/화 중에 두번째 요청사항 들어감!

## Detailed Methods

### Image Processing

| Feature Type                |
| --------------------------- |
| SIFT                        |
| ORB                         |
| KAZE                        |
| AKAZE                       |
| BRISK                       |
| FAST(TODO)                  |
| superglue/superpoint (TODO) |
| HardNet (TODO)              |




| Image Processing            | Frontend | Backend | Loop Closure |
| --------------------------- | -------- | ------- | -------- |
|                  |          |         |              |
|                  |          |         |              |
|                  |          |         |              |
|                  |          |         |              |
|                  |          |         |              |
|                  |          |         |              |
|                  |          |         |              |
|                  |          |         |          |

- Keypoint Detection
  - Moravec, Harris, SIFT, FAST, oFAST(ORB), AKAZE, SuperPoint, KeyNet

- Descriptor Extraction

  - SIFT, BRIEF, rBRIEF(ORB), AKAZE, SuperPoint, HardNet

  - Floating point descriptor, Binary descriptor


- Correspondence Matching

  - FLANN-based Matcher (KDTree, Randomized Tree, ...)

  - Brute-Force Matcher

## Algorithm Overview
### Base Algorithm - ProSLAM
![PROSLAM](https://user-content.gitlab-static.net/c5cc03f792d716a40027d00c427f54b5f3cd26df/68747470733a2f2f64726976652e676f6f676c652e636f6d2f75633f6578706f72743d646f776e6c6f61642669643d315538534a75455476627459677147465649506666555077492d69696b53733473)

### Comparsion Algorithm : ORB-SLAM2

![ORB-SLAM2-PIPELINE](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ZWXY3coSBymuqZnv9RZM4g.png)


| 2                                                            | 3                                                            | 4(토)                                                        | 5(일)                                                | 6                                                    | 7                                                            | 8 <중간점검>                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| 영상처리 : Feature, Descriptor <br />백엔드 : 자료조사.<br />프론트 : 자료조사. 요구사항, 이미지프로세싱에게 받아야 하는 정보, 백엔드에게 전달해야하는 정보<br />아키텍트 : 자료조사.<br /> | 영상처리 : Descriptor <br />백엔드/프론트 : ORB-SLAM2 조사 및 구현<br />아키텍트 : ORB-SLAM2 UML<br /><br /><br />백/프 1시 미팅<br />18시 강사님 미팅 | 영상처리<br />백엔드<br />프론트<br />아키텍트<br />Docker Image 생성 | 영상처리<br />백엔드<br />프론트<br />아키텍트<br /> | 영상처리<br />백엔드<br />프론트<br />아키텍트<br /> | 영상처리<br />백엔드<br />프론트<br />아키텍트<br />중간 점검용 DOC<br /><br />강사님 미팅 (1번 요청사항) | 영상처리<br />백엔드<br />프론트<br />아키텍트<br /> |
| 9                                                            | 10                                                           | 11(토)                                                       | 12(일)                                               | 13                                                   | 14                                                           | 15                                                   |
| 영상처리<br />백엔드<br />프론트<br />아키텍트<br />         | 영상처리<br />백엔드<br />프론트<br />아키텍트<br />         | 영상처리<br />백엔드<br />프론트<br />아키텍트<br />         | 영상처리<br />백엔드<br />프론트<br />아키텍트<br /> | 테스트<br />DOC                                      | 테스트<br />DOC                                              | 테스트<br />발표                                     |

높은 우선 순위

- KITTI 데이터셋에서 돌 수 있게 프레임워크 개량 (+50점)
- 포즈 추정 정확도 개선 (+50점)
  -  오픈소스를 참고해 직접 VSLAM 파이프라인을 설계 및 구현 – 최소 2 모듈 이상 변경 (+150점)
- 오프라인 시각화 가능 (+50점)
- 아키텍처 / 알고리즘 재사용성 개선 (+100점)

낮은 우선 순위

- PC 웹캠 / 리얼센스 카메라로 돌 수 있게 프레임워크 개량 (+100점)
- 자이카에서 돌 수 있게 프레임워크 개량 (+100점)
- 프레임당 연산 속도 개선 (+50점)
- 실시간 시각화 가능 (+50점) - RVIZ
- 안정성 확보 – CI/CD + 유닛테스트 검증 (+100점)

## REFERENCES
https://arxiv.org/abs/1610.06475
https://arxiv.org/abs/1709.04377
https://jakobengel.github.io/pdf/engel14eccv.pdf
https://github.com/mateomd-dev/orb-slam2
https://gitlab.com/srrg-software/srrg_proslam

## 최종 발표  
https://south-spruce-3f7.notion.site/Team3-SLAM-95ee72fda0c04ffa9ec51e468793eac9
