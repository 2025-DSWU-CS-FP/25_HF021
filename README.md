# Eyedia <img src="https://eyedia.netlify.app/logo.svg" width="110" align="left" />
LLM과 RAG 기술을 활용한 AI기반 미술관 도슨트 서비스

<br />

## **💡1. 프로젝트 개요**

**1-1. 프로젝트 소개**
- 프로젝트 명 : LLM과 RAG 기술을 활용한 AI기반 미술관 도슨트 서비스
- 프로젝트 정의 : 사용자가 시선 추적을 통해 원하는 부분만 질의하면, AI로 해당 부분에 대한 설명을 찾아서 답변해주는 대화형 도슨트 서비스

<img width="1708" height="960" alt="image" src="https://eyedia.netlify.app/image.png" /></br>

<br />

**1-2. 개발 배경 및 필요성**

본 프로젝트는 스마트 아이웨어(라즈베리파이) , LLM(대형 언어 모델), RAG(문서 검색 기반 생성 모델)을 활용하여 AI 기반 미술관 도슨트 시스템을 개발합니다. 사용자가 웹 환경에서 미술관의 특정 그림, 특정 객체에 대해 질문하면, 그에 대한 자연스럽고 자세한 설명을 제공합니다. 

<br />

**1-3. 프로젝트 특장점**
- 실시간 맞춤형 AI 도슨트
- 시선·관심 객체·음성 질의 등 다양한 입력을 수집·해석해 즉석 설명 생성
- 채팅·음성(TTS)로 결과 제공, 관람 흐름에 맞춘 인터랙티브 경험 제공
- 미리 녹음된 일방향 설명·GPS/QR/버튼 입력 중심의 기존 도슨트 방식에서 탈피
- 시선 추적·객체 인식·멀티모달 AI(영상·음성·텍스트 통합)로 관람객의 ‘관심’과 ‘행동’ 중심 설계
- 상용 안내기의 폐쇄성·고가 대비, 오픈소스 기반으로 기능 자유 추가·변경·확장 가능
- 시선(동공)·환경(작품)·음성(질의)·프론트 클릭 등 모든 입력을 실시간 통합 분석
- 진정한 맞춤형 도슨트 경험 구현, 현장 적용 가능성과 확장성 입증

<br />


**1-4. 주요 기능**
- 객체 인식·크롭 자동화: Ultralytics YOLOv8로 작품 내 객체 bbox 탐지 → OpenCV로 객체별 crop 저장/라벨 매핑
- 임베딩 기반 유사도 검색: CLIP 임베딩 + FAISS 코사인 유사도 검색으로 가장 유사한 객체와 설명을 자동 반환
- LLM 도슨트 설명 생성: GPT-4o에 프롬프트 전달 → 한국어 구어체 설명 생성 → 채팅 형식으로 백엔드 전송(FastAPI)
- 시선 추적·객체 선택(Gaze): OpenCV/MediaPipe로 동공 중심 추출 → Homography 기반 Gaze Mapping → YOLO bbox와 교차해 ‘응시 객체’ 판정 및 시선 시각화
- 실시간 멀티모달 파이프라인: Raspberry Pi가 환경/동공 영상+음성 수집→ Wi-Fi로 FastAPI 전송 → YOLO·CLIP·FAISS 처리 → STT/TTS → Spring Boot 저장/권한 → React 채팅 UI
- 스마트 아이웨어 H/W: Pi 5(8GB) + Camera Module 3(환경) + Camera Module 3 NoIR(적외선·눈동자) + ReSpeaker 2-Mics Pi HAT(마이크/스피커) + Wi-Fi
- 음성 입출력 연동: 마이크로 STT용 입력→ 서버 처리 → TTS 결과를 스피커로 재생(장치 불량 교체 진행 메모 포함)
- 실시간 통신/데이터 연동: Raspberry Pi ↔ 백엔드 간 실시간 송수신(영상/시선/음성), 연동 완료
- 클라우드 데이터 관리: 이미지/메타데이터는 S3, 관계 데이터는 RDS(MySQL)에 안전 저장
- 웹앱 주요 기능: 메인/갤러리 감상, 스마트 아이웨어 연동 채팅, 대화 기록 확인·검색, 발췌 기능

<br />

**1-5. 기대 효과 및 활용 분야**

기대 효과
> 관람객의 시선·질의·행동을 토대로 해설을 즉시 생성해 기존 오디오 가이드보다 몰입감과 만족도를 높이고, 시선·질문·체류시간 등 행동 데이터를 축적·분석해 큐레이션과 동선 설계를 지속적으로 개선할 수 있습니다. 텍스트·음성(TTS)을 동시 제공해 연령·장애 유무와 상관없이 접근성을 강화하고, 웹(React)·백엔드(Spring) 기반 구조와 오픈소스 모듈러 설계로 현장/장비 제약 없이 빠른 배포와 기능 확장이 가능합니다. 팀과 기관 입장에서는 YOLO·CLIP·LLM·시선추적 등 융합 기술을 실전에서 다루며 운영 자동화 파이프라인을 축적해 인력·비용 효율을 동시에 확보합니다.

활용 분야
> 미술관·박물관·기념관 등 전시 공간에서 작품 맞춤 도슨트로 즉시 적용할 수 있고, 과학관·기업 쇼룸·브랜드 팝업/리테일 전시에서는 제품·프로토타입 이해를 돕는 인터랙티브 설명으로 전환율을 높일 수 있습니다. 도시 관광지·문화재 현장·야외 페스티벌/비엔날레에서는 GPS·비전 결합 안내로 현장성을 강화하고, 학교·대학·도서관·공공기관에서는 교육용 체험형 콘텐츠와 접근성 보조 해설로 학습 효과를 높입니다. 공항·역사·박람회 같은 대규모 유동 인프라에서는 다국어 안내와 군중 행태 데이터 분석에, 스마트 아이웨어와 결합한 투어·이벤트 운영에는 경량 장비 기반의 이동형 가이드로 확장 가능합니다.

<br />

**1-6. 기술 스택**
- 프론트엔드 : React, Typescript, Tanstack Query Tailwind CSS
- 백엔드 : Spring Boot
- AI/ML : OpenAI API, Python(FastAPI)
- 데이터베이스 : 
- 클라우드 : AWS
- 배포 및 관리 : Docker, GitHub Actions, Netlify

---

## **💡2. 팀원 소개**
| [<img src="https://github.com/Dubabbi.png" width="150px">](https://github.com/Dubabbi) | [<img src="https://github.com/kcw9609.png" width="150px">](https://github.com/kcw9609) | [<img src="https://github.com/20210699.png" width="150px">](https://github.com/20210699) | [<img src="https://github.com/chaemin.png" width="150px">](https://github.com/chaemin) | [<img src="https://github.com/Yooni.png" width="150px">](https://github.com/Yooni) |
|:---:|:---:|:---:|:---:|:---:|
| [윤소은](https://github.com/Dubabbi)   | [강채원](https://github.com/kcw9609)   | [김예빈](https://github.com/20210699) | [유채민](https://github.com/chaemin) | [이윤서](https://github.com/Yooni) |
| • 팀장 <br> • 프론트엔드 | • 부팀장, 백엔드 총괄 <br> • 백엔드, 모델  | • 서기 <br> • CI/CD 구축, 백엔드, 모델 |• 비교과 총괄, 작업/보고서 관리 <br> • 백엔드 | • llm & 데이터분석 파트장 <br> • 백엔드/모델 |



---
## **💡3. 시스템 구성도**


| 서비스 구성도 | 시스템 구성도 | 엔티티 관계도 | 아이웨어 연결 → 실시간 채팅 flow |
|---------------|---------------|---------------|-----------------------------------|
| <img width="160" alt="서비스 구성도" src="https://github.com/user-attachments/assets/b92dc6fe-0805-4f94-b179-313b86f62f24" /> | <img width="100" alt="시스템 구성도" src="https://github.com/user-attachments/assets/076db477-f6f9-4374-8a2c-84172518cde0" /> | <img width="315" alt="엔티티 관계도" src="https://github.com/user-attachments/assets/88d41b68-86a5-4132-bf8e-b8e4db92c87f" /> | <img width="290" alt="실시간 채팅 flow" src="https://github.com/user-attachments/assets/866d1f77-218b-4d0e-87de-4d3f139cc9fb" /> |

---
## **💡4. 작품 소개영상**

[![Eyedia 프로젝트 소개](https://eyedia.netlify.app/image.png)](https://www.youtube.com/watch?v=akFH7fvptO8)

---
## **💡5. 핵심 소스코드**
- 소스코드 설명 : 추가하기

```Java
코드 추가하기!!
```
