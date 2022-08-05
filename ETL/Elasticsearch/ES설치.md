# ES 설치 (ver.2022.08)

## 환경
- LINUX
<br>

## 설치 패키지 다운로드
#### 최신 버전 다운로드 https://www.elastic.co/kr/downloads/elasticsearch
#### 모든 버전 다운로드 https://www.elastic.co/kr/downloads/past-releases#elasticsearch 

```
// 패키지 다운로드
curl -LO https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-{버전}-linux-x86_64.tar.gz

// 압축파일 풀기
tar -xzf elasticsearch-{버전}-linux-x86_64.tar.gz
```
<br>

## ES 실행
```
bin/elasticsearch
```
Elasticsearch 실행 시, 추가 옵션 사용 가능<br>
- `bin/elasticsearch -d` <br> 백그라운드 데몬 실행 옵션<br>
- `bin/elasticsearch -p <파일명>` <br> ES 프로세스 ID를 지정한 파일에 저장 <br> 실행 종료시, 파일은 자동으로 삭제됨<br>

## 환경 설정
개발에서 ES 노드를 2개 이상 띄워야할 경우, <br>
ES 노드당 각각 java 메모리를 할당하므로 메모리 부족 이슈가 발생할 수 있음.
jvm heap size를 1g로 정해주어야함.

```
#설정 파일로 이동
vi config/jvm.options
 
#라인추가 / heep size 변경
-Xms1g 
-Xmx1g
```
