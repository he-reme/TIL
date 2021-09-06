# PySpark

> Apache Spark 기능을 사용하여 Python 애플리케이션을 실행하기 위해 Python으로 작성된 Spark 라이브러리
>
> `sparkexam.ipynb` 참고..

* Py4JpySpark 내에 통합된 Java 라이브러리이며, Python이 JVM 개체와 동적으로 인터페이스 할 수 있도록 하므로
  * PySpark를 실행하려면
  * Python 뿐만 아니라 Java개발환경(JDK)도 설치되어 있어야 함

* 개발을 위해 Spyder IDE, Jupyter lab과 같은 많은 유용한 도구와 함께 제공되는 Anaconda 배포를 사용하여 PySpark 애플리케이션을 실행할 수 있

* 대규모 데이터셋을 효율적으로 처리하기 때문에
  * Numpy, Pandas, TensorFlow를 포함하여 Python으로 작성된 데이터 과학 라이브러리와 함께 많이 사용됨

#### 장점

* 분산 방식으로 데이터를 효율적으로 처리할 수 있는 메모리 분산 처리 엔진
* PySpark에서 실행되는 애플리케이션은 기존 시스템보다 100배 빠름
* 데이터 수집 파이프 라인에 PySpark를 사용하면 큰 이점을 얻을 수 있음
* Hadoop HDFS, AWS s3 및 여러 파일 시스템의 데이터를 처리 할 수 있음
* Streaming 및 Kafka를 사용하여 실시간 데이터를 처리하는데도 사용
* 스트리밍을 사용하면 파일 시스템에서 파일을 스트리밍하고 소켓에서 스트리밍 할 수 있음
* 기본적으로 기계 학습 및 그래프 라이브러리가 있음

#### PySpark 아키텍처

* Apache Spark는 마스터-슬레이브 아키텍처에서 작동
  * 마스터 : 드라이버
  * 슬레이브 : 작업자
* Spark 애플리케이션을 실행하면 Spark Driver가 애플리케이션의 진입점인 컨텍스트를 생성하고
* 모든 작업(변환 및 작업)이 작업자 노드에서 실행되고
* 리소스는 Cluster Manager에서관리됨



---



