# OCR 사용을 위한 Vision API 사용

### Google Cloud SDK 다운로드

- 압축 파일 다운로드 및 압축 해제
  https://cloud.google.com/sdk/docs/quickstarts

- 설치
  ```
  (자신의 google-cloud-sdk의 상위주소)/google-cloud-sdk/install.sh
  ```

- 설정 파일 경로 기억
  ```
  Enter a path to an rc file to update, or leave blank to use [file path]:
  ```

- 설정파일 적용
  ```
  source [file path]
  ```

- Google Cloud SDK 초기화
  ```
  gcloud init
  ```

- 자신의 계정과 프로젝트를 등록

- API 사용을 위한 계정 및 키 생성
  - IAM & Admin 서비스 계정 생성
  - Keys Json 파일 추가

- 설정파일 path에 json key 경로 추가
```
export COOCLE_APPLICATION_CREDENTIALS="/Users/maenoh/Documents/key/ocr-test-365301-45ccca0a07f7.json"
```

