# pillDetection
🚀 2025 컴퓨터비전 프로젝트

### 프로젝트 개요
복잡한 이미지 환경에서 다중 알약을 탐지하고, 형상·색상·각인·분할선 등 다중 시각 특징을 분석하여 경구약제를 자동 식별하는 시스템

### 파일 구조
```commandline
pillDetection/
├── weights/                              # 학습된 모델 가중치
├── images/                               # 경구약제 조합 이미지
├── drug_info_unique_drug_id_final.csv    # 약품 정보 데이터베이스
├── demo.ipynb                            # 최종 알약 탐지 파이프라인
├── merge_coco_to_yolo.ipynb              # COCO→YOLO 데이터 변환
├── YOLO_augmentation.ipynb               # YOLO 데이터 증강
├── resnet_training.ipynb                 # ResNet-50 형상/색상 분류 학습
├── pill_matching_results.xlsx            # 매칭 결과
├── requirements.txt                      # 필요 라이브러리
└── README.md
```

### 시스템 구성
1. **YOLO 기반 다중 알약 탐지**: YOLOv12n으로 이미지 내 알약 ROI 검출
2. **ResNet-50 특징 추출**: 형상(4 클래스), 색상(7 클래스) 분류
3. **OCR 각인 인식**: EasyOCR + Google Vision API
4. **다중 특징 매칭**: 가중치 기반 최종 약품 식별

## 성능
| 모델 | 지표 | 성능 |
|------|------|------|
| YOLO | mAP50 | 0.971 |
| YOLO | Recall | 0.934 |
| ResNet-50 (형상) | Accuracy | 0.9070 |
| ResNet-50 (색상) | Accuracy | 0.7907 |
| 최종 매칭 | Top-5 Accuracy | 44.68% (4023종 대상) |

## 데이터셋
- 한국지능정보사회진흥원 제공 "경구약제 이미지 데이터" 활용
- Roboflow Universe의 공개 데이터셋인 Roboflow 100 pills'와 'seblful Pills Detection'을 활용

## 실행 환경
- Python 3.x
- PyTorch
- Ultralytics YOLO
- EasyOCR
- demo.ipynb 코드에서 `## 6️⃣ 파이프라인 초기화` 부분에서, Google Vision API key를 넣어야 OCR Fallback이 실행됩니다. 