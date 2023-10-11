# Apache Kafka 사용법

## Kafka란?
- 분산 데이터 스트리밍 플랫폼
- 주요 특징
  - 분산 메세지 큐: Topic 단위로 메세지 큐를 구성되며, 해당 Topic은 여러 파티션 분할이 가능하고 여러 브로커(서버)에서 처리할 수 있음
  - 내구성과 확장성: 데이터를 안전하게 저장, 복제를 하여 내구성을 확보하고, 손쉬운 브로커 추가를 통한 확장을 이룰 수 있음
  - 이벤트 스트리밍
  - 대용량 데이터 처리
  - 높은 성능
  - 다양한 클라이언트 지원

## Apache Kafka CLI source 다운로드
```bash
sudo apt-get update
sudo apt-get install openjdk-11-jre # java 실행환경 설치
wget https://downloads.apache.org/kafka/3.6.0/kafka-3.6.0-src.tgz # 작성 기준 최신 안정화 버전: 3.6.0
tar -xzf kafka-3.6.0-src.tgz
```

## CLI 기반 Kafka 사용법
0. 실행 쉘 스크립트들이 위치한 bin 디렉토리로 이동
```bash
cd kafka-3.6.0-src.tgz # kafka 압축 해제 디렉토리 이동
cd bin # 실행파일 저장 디렉토리 이동
```

1. Zookeeper 실행(새 bash shell에서)
```bash
./zookeeper-server-start.sh ../config/zookeeper.properties # zookeeper 설정 파일을 바탕으로 zookeeper서버 실행
```

2. Kafka 서버 실행(새 bash shell에서)
```bash
./kafka-server-start.sh ../config/server.properties # kafka 설정 파일을 바팡으로 kafka서버 실행
```

3. Kafka topic 생성(새 bash shell에서)
```bash
./kafka-topics.sh --create --topic test_topic --partitions 1 --replication-factor 1 --bootstrap-server localhost:9092
```

4. 생성한 topic을 기반으로 Producer 실행
```bash
./kafka-console-producer.sh --topic test_topic --bootstrap-server localhost:9092
```
  이후 하단에 나오는 입력창에서 타이핑을 진행할 시 cache에 저장됨.  

5. 생성한 topic을 기반으로 Consumer 실행(새 bash shell에서)
```bash
./kafka-console-consumer.sh --topic test_topic --from-beginning --bootstrap-server localhost:9092
```
  이후 여태까지 입력해 두었던, 이벤트 메세지들이 처음부터 출력되며 실시간 Producer-Consumer 통로가 생성됨.  

6. Topic 삭제 방법
```bash
./kafka-topics.sh --delete --topic test_topic --bootstrap-server localhost:9092
```

etc. Topic 정보 조회
```bash
./kafka-topics.sh --describe --topic test_topic --bootstrap-server localhost:9092
```