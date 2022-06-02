# ktds-edu
ktds Container 기반 istio, argocd 교육자료



# 서비스메쉬와 ArgoCD기반 CICD(6/13)







# 1. Class1: kubernetes ( [가이드 문서보기](./kubernetes/kubernetes.md) )  





## 1) Kubernetes 란 무엇인가?

- k8s 개요

- k8s 이전에는?

- 왜 k8s 가 필요한가?





## 2) 실습 환경 설명

- mobaxterm
- wsl
- docker desktop 확인
- KT Cloud 서버





## 3) Docker 실습

- sample app 실행
- Scale Out
- 부하분산 고민
- clean up



## 4) k3s 실습(개인PC)

- k3s 란?
- wsl 에 k3s 설치
- sample app deploy



## 5) K3s 실습(KT Cloud)

- k3s 설치(참고)
- 개인 Namespace 확인
- Sample app deploy







# 2. Class2: ServiceMesh ( [가이드 문서보기](./istio/ServiceMesh.md) )  



## 1) Service Mesh 란?



## 2) Istio 란?



## 3) 실습(개인PC)

- helm 설치
- helm 을 이용한 Istio 설치
- sample app sidecar inject
  - userlist application을 활용하여 istio sidecar inject 에 대한 이해도를 높인다.



## 4) 실습(KT Cloud-기본)

- sample app (bookinfo) install
  - bookinfo application 을 활용한 실습을 통해서 istio 를 이해한다.
  - bookinfo 는 온라인 서점의 단일 카탈로그 항목과 유사한 도서에 대한 정보를 표시하는 app 이다.
- Monitoring
  - Grafana
  - Kiali
  - Jaeger



## 5) 실습(KT Cloud-Traffic control)

- Traffic Shifting
  - 서비스별로 트래픽의 가중치를 조정하므로서 특정 버전에서 다른 버전으로 트래픽을 이동하는 방법을 제어할 수 있다.
- Request Routing
  - 여러 버전의 마이크로서비스로 동적으로 라우팅하는 방법을 확인할 수 있다.
- Fault Injection
  - application 의 복원력을 테스트하기 위해서 결함을 주입할 수 있다.
- Circuit Breaking
  - istio는 Connection pool 과   Load balancing pool 기반의 circuit breaking 기능을 제공한다.







# 3. Class3: ArgoCD ( [가이드 문서보기](./argocd/argocd.md) )  



## 1) GitOps



## 2) ArgoCD 이론



## 3) 실습(개인PC)

- wsl 에 argocd 설치
- ArgoCD Project 구성(sample app)
- Sync 및 접속확인



## 4) 실습(KT Cloud)

- ArgoCD Project 구성(개인 NS에 userlist 배포)
- 동일Project 구성
- Sync 및 접속확인
- rgo-rollout 테스트
- app in apps pattern 테스트 ??







