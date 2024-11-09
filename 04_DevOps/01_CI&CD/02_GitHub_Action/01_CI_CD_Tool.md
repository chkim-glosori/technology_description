# CI/CD Tool

## 1. CI/CD Tool 이란?
CI/CD(Continuous Integration/Continuous Deployment 또는 Continuous Delivery) 도구는 소프트웨어 개발 프로세스를 자동화하여 코드 변경 사항을 지속적으로 통합하고, 테스트하며, 배포하는 데에 도움을 주는 도구이다.

## 2. CI/CD Tool 별 장/단점 분석

### 2-1. Jenkins
#### 장점
- 오픈 소스이며 플러그인 생태계가 풍부하여 다양한 도구와 통합이 가능하다.
- 유연한 설정과 커스터마이징이 가능하다.
- 대규모 프로젝트와 팀에 적합하다.

#### 단점
- 어렵다.
- 초기 설정과 유지 관리가 복잡하다.
- 서버 관리가 필요하며, 클라우드 기반 솔루션(GitHub Action) 에 비해 인프라 관리 부담이 크다.

### 2-2. GitHub Actions
#### 장점
- GitHub 와 통합이 뛰어나며, GitHub 레파지토리에 쉽게 설정이 가능하다.
- YAML 기반의 간단한 설정으로 사용하기 쉽다.
- 다양한 액션을 통해 다양한 작업을 자동화할 수 있다.

#### 단점
- GitHub 에 의존하게 되며, 다른 플랫폼과의 통합이 제한적이다.
- 복잡한 워크플로우에서는 설정이 어려울 수 있다.

## 3. 내가 사용할 CI/CD Tool
Jenkins 는 다뤄야 할 부분들이 굉장히 많은 것으로 들었다. GitHub Action 을 사용하면서 CI/CD 를 프로젝트에 적용해 보려고 한다.