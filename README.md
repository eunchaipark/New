---

### **프로젝트 이름: 날씨와 경제 데이터를 활용한 범죄율 예측 시스템**

**목표:**

날씨와 경제 조건이 범죄율에 미치는 영향을 분석하고, 이를 바탕으로 범죄 발생 확률을 예측하는 시스템을 구축하여 범죄 예방 및 대응 계획 수립을 돕는 대시보드 제공.

---

### **1단계: 데이터 수집**

**필요 데이터 및 API**

- **날씨 데이터**
    - **API:** OpenWeatherMap API
    - **데이터 항목:** 온도, 강수량, 습도, 기압 등
    - [OpenWeatherMap API](https://openweathermap.org/api)
- **경제 데이터**
    - **API:** FRED (Federal Reserve Economic Data) API 또는 경제 관련 공공 API
    - **데이터 항목:** GDP 성장률, 실업률, 소비자 물가 지수(CPI) 등
- **범죄 데이터**
    - **API:** FBI Crime Data API
    - **데이터 항목:** 범죄 유형, 발생 시간, 위치 등
    - [FBI Crime Data API](https://api.usa.gov/crime/fbi/cde)

---

### **2단계: 데이터 저장**

- **AWS 서비스 사용**
    - **AWS S3**
        - 데이터 저장 위치 구성:
            - `/raw/weather/`: 날씨 원시 데이터 저장
            - `/raw/economy/`: 경제 원시 데이터 저장
            - `/raw/crime/`: 범죄 원시 데이터 저장
            - `/processed/`: 처리된 데이터 저장

---

### **3단계: 데이터 처리 및 분석**

- **데이터 전처리**
    - **AWS Glue**
        - Null 값 제거, 중복 데이터 처리
        - 날씨, 경제, 범죄 데이터를 시간 및 지역 기준으로 병합
- **데이터 분석 및 예측 모델 개발**
    - **AWS Athena**
        - S3에 저장된 데이터를 SQL 쿼리로 분석
    - **AWS SageMaker**
        - **모델 유형:**
            - **랜덤 포레스트**: 날씨, 경제, 범죄 간 상관관계 분석
            - **XGBoost**: 범죄 발생 확률 예측
        - **학습 데이터:**
            - 입력: 날씨 데이터(온도, 강수량 등), 경제 데이터(GDP, 실업률 등)
            - 출력: 범죄 발생 여부 및 유형

---

### **4단계: 예측 결과 저장 및 알림 시스템**

- **AWS 서비스 사용**
    - **Amazon DynamoDB**
        - 예측 결과 저장 (지역별, 날짜별)
    - **Amazon SNS (Simple Notification Service)**
        - 예측된 범죄 발생 확률이 높은 경우 알림 발송

---

### **5단계: 데이터 시각화**

- **AWS 서비스 사용**
    - **Amazon QuickSight**
        - 대시보드 구성:
            - 지역별 날씨 및 경제와 범죄율 간 트렌드 시각화
            - 특정 날씨와 경제 조건에서 범죄 발생 확률 예측
            - 시간대별, 범죄 유형별 데이터 필터링 기능 제공

---

### **6단계: 배포 및 운영**

- **AWS 서비스 사용**
    - **AWS CloudFormation**
        - 인프라 자동화 및 배포
    - **AWS Cost Explorer**
        - 비용 모니터링 및 최적화

---

### **최종 시스템 구조**

1. **데이터 수집**:
    - OpenWeatherMap, 경제 관련 API, FBI Crime API를 통해 Lambda 및 Glue가 데이터를 S3에 저장
2. **데이터 처리**:
    - Glue와 Athena를 사용하여 데이터를 정제하고 분석
3. **모델 학습 및 예측**:
    - SageMaker에서 예측 모델을 학습하고 배포
4. **결과 저장 및 알림**:
    - DynamoDB로 예측 결과 저장, SNS로 알림 발송
5. **시각화 및 배포**:
    - QuickSight로 대시보드 구성, CloudFormation을 통해 배포

---

### **프로젝트 일정**

1. **1주차**: 데이터 소스 및 AWS 서비스 설계
2. **2주차**: 날씨 및 경제 데이터 수집 및 S3 저장 구현
3. **3주차**: 데이터 전처리 및 모델 학습 구현 (SageMaker)
4. **4주차**: 예측 결과 저장 및 QuickSight 대시보드 제작
5. **5주차**: 최적화 및 배포

---

### **참고사항**

- 날씨와 경제는 범죄 발생에 영향을 미치는 주요 변수로 가정하되, 추가적인 변수(예: 사회적 요인, 정책 변화 등)도 고려할 수 있음.
- 데이터의 정확성 및 신뢰성 확보가 중요하며, 각 API의 데이터 업데이트 주기 및 정확성에 따라 모델의 성능이 달라질 수 있음.
