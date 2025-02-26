# Elastic Search

## 1. Elastic Search 란
Elastic Search 는 Apache Lucene 기반의 분산형 검색 엔진으로, 실시간 검색과 데이터 분석을 위해 설계되었다. 대량의 데이터를 빠르게 검색하고, 복잡한 쿼리를 수행할 수 있는 기능을 제공한다.

JSON 형식의 RESTful API 를 통해 데이터를 색인하고 검색할 수 있으며, 데이터의 구조화 및 비구조화에 모두 적합하다.

[주요 특징]
- 대량의 데이터를 여러 서버에 분산하여 처리할 수 있다.
- 데이터가 색인된 후에 거의 즉시 검색이 가능하다.
- 다양한 프로그래밍 언어에서 쉽게 사용할 수 있도록 RESTful API 로 설계되었다.
- 복잡한 검색 조건을 표현할 수 있는 쿼리 DSL 을 제공한다.

### 쿼리 DSL
쿼리 DSL (Query Domain Specific Language) 은 특정 도메인이나 데이터베이스를 위해 설계된 쿼리 언어로, 주로 데이터 검색 및 조작을 위한 명령어 집합을 제공한다. Elastic Search 같은 검색 엔진에서는 사용자가 데이터를 효과적으로 검색할 수 있도록 다양한 쿼리 옵션을 제공하는 쿼리 DSL 을 제공한다.

## 2. Elastic Search 가 제공하는 기능
- Full-Text Search: 텍스트 기반의 데이터에 대해 강력한 검색 기능을 제공합니다.
- 자동 완성: 사용자가 입력하는 도중에 추천 검색어를 제공할 수 있는 기능.
- 집계(aggregation): 데이터를 그룹화하고 요약하여 분석할 수 있는 기능.
- 지리적 검색: 지리적 좌표를 기반으로 한 검색 기능을 지원합니다.
- 다양한 데이터 타입: JSON 형식으로 다양한 데이터 타입을 지원합니다.
- 스케일 아웃: 필요에 따라 노드를 추가하여 쉽게 확장할 수 있습니다.

## 3. Django 의 Search 와의 차이점
Django 의 검색 기능과 Elastic Search 는 모두 검색 기능을 제공하지만, 규모와 용도에서 차이를 보인다.

### 3-1. 성능 및 확장성
Elastic Search 는 대량의 데이터를 처리하는 데 최적화되어 있으며, 분산형 아키텍처를 통해 성능을 극대화한다. 반면 Django 의 검색 기능은 주로 데이터베이스의 쿼리를 사용하여 검색을 수행하며, 데이터의 규모가 커질수록 성능이 저하될 수 있다.

### 3-2. 기능의 다양성
Elastic Search 는 복잡한 쿼리, 집계, 자동 완성 기능 등 다양한 검색 기능을 제공한다. Django 의 검색 기능은 기본적인 텍스트 검색을 중심으로 하며, PostgreSQL 의 Full-Text Search 기능을 활용하는 경우가 많다

### 3-3. 사용 용도
Elastic Search 는 검색, 로그 분석, 데이터 분석 등의 다양한 용도로 사용되지만, Django 의 검색 기능은 주로 웹 애플리케이션 내에서 사용자 쿼리 처리에 초점을 맞춘다.

### 요약
전반적으로 Elastic Search 는 로그, 데이터 분석 등 '다양한 범위'에 자동 완성, 집계, 복잡한 쿼리와 같은 '다양한 기능' 을 제공하는 것으로 생각해 볼 수 있다. 단순히 웹 애플리케이션에서 적은 데이터를 다룰 것이 아니라면, Elastic Search 를 꼭 써보는 게 좋겠다.

## 4. Elastic Search 를 사용할 때 유의할 점
- 데이터 모델링: Elastic Search 는 데이터의 구조화 및 비구조화를 지원하지만, 데이터 모델링을 잘못하면 검색 성능이 저하될 수 있다. 적절한 인덱스와 필드 매핑을 설정하는 것이 중요하다.

- 스케일링: Elastic Search 는 분산형 아키텍처를 사용하므로, 서버를 추가하거나 재구성할 때 고려해야 할 점이 많다. 데이터 샤딩 및 복제 설정을 잘 이해하고 구성해야 한다.

- 보안: Elastic Search 는 기본적으로 인증 및 권한 부여가 설정되어 있지 않으므로, 운영 환경에서는 적절한 보안 설정을 적용해야 한다. X-Pack과 같은 플러그인을 사용하여 보안을 강화할 수 있다.

- 모니터링 및 유지 관리: Elastic Search 클러스터의 상태를 모니터링하고, 성능을 유지하기 위해 정기적인 유지 관리가 필요하다. 이를 위해 Kibana 와 같은 도구를 사용할 수 있다.

- 백업 및 복구: 데이터 손실을 방지하기 위해 정기적인 백업과 복구 전략을 마련해야 한다.