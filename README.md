# pillDetection
🚀 2025 컴퓨터비전 프로젝트

### 프로젝트 개요
복잡한 이미지 환경에서 다중 알약을 탐지하고, 형상·색상·각인·분할선 등 다중 시각 특징을 분석하여 경구약제를 자동 식별하는 시스템

### 파일 구조
```commandline
pillDetection/
├── images/                               # 테스트용 알약 이미지 폴더
├── output/                               # 시각화·결과 저장 폴더
├── utils/                                # 학습/전처리 관련 유틸 노트북
│   ├── merge_coco_to_yolo.ipynb          # COCO → YOLO 포맷 변환
│   ├── resnet_training.ipynb             # ResNet-50 형상·색상 분류 학습
│   └── YOLO augmentation.ipynb           # YOLO 학습용 데이터 증강
├── weights/                              # 학습된 모델 가중치
│   ├── best.pt                           # YOLO 최종(best) 가중치
│   ├── last.pt                           # YOLO 마지막 에폭 가중치
│   ├── pill_shape_color_resnet50_improved_best_color.pth  # 색상 분류기
│   └── pill_shape_color_resnet50_improved_best_shape.pth  # 형상 분류기
├── .gitignore                            # Git 무시 파일 설정
├── demo.ipynb                            # 통합 알약 탐지·식별 데모 노트북
├── drug_info_unique_drug_id_final.csv    # 약품 메타데이터 DB
├── K-000250-000573-002483-006192_0_2_0_2_70_000_200.png   # 샘플 조합 이미지
├── pill_matching_results.csv             # 매칭 결과(텍스트 버전)
├── pill_matching_results.xlsx            # 매칭 결과(엑셀 버전)
├── README.md                             # 프로젝트 사용 설명
├── requirements.txt                      # 의존 라이브러리 목록
└── team8_presentation.pdf                # 팀 발표 자료 PDF

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