

# 서비스메쉬와 ArgoCD기반 CICD

> ktds Container 기반 istio, argocd 교육자료

본 교육은 Container를 기반으로 한 ServiceMesh(istio), argocd CICD 를 학습하는 과정으로 docker, kubernetes, istio, git, argocd, grafana, kiali, jeager 등 다양한 솔루션들에 대해서 알아보며 각각 실습을 수행한다.

문의: 송양종( yj.song@kt.com / ssongmantop@gmail.com )








# 1. 시작전에 ( [가이드 문서 보기](./beforebegin/beforebegin.md) )  



## 1) 실습 환경 준비(개인PC)

- 실습에 필요한 tool 준비
  - mobaxterm 확인
  - wsl
  - docker desktop 확인

- 교육자료 Download



## 2) 실습 환경 준비(개인PC)

- KT Cloud 이해
- ssl 접속 확인
- 수강생별 계정 매핑
- 교육자료 Download






# 2. Class1: kubernetes 맛보기 ( [가이드 문서 보기](./kubernetes/kubernetes.md) )  



## 1) Kubernetes 란 무엇인가?

- k8s 개요

- k8s 이전에는?

- 왜 k8s 가 필요한가?



## 2) Docker 실습

- sample app 실행
- Scale Out
- 부하분산 고민
- clean up



## 3) k3s 실습(개인PC)

- k3s 란?
- wsl 에 k3s 설치
- sample app deploy



## 4) K3s 실습(KT Cloud)

- k3s 설치(참고)
- 개인 Namespace 확인
- Sample app deploy







# 3. Class2: ServiceMesh ( [가이드 문서 보기](./istio/ServiceMesh.md) )  



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
  - Grafana / Kiali / Jaeger



## 5) 실습(KT Cloud-Traffic control)

- Traffic Shifting
  - 서비스별로 트래픽의 가중치를 조정하므로서 특정 버전에서 다른 버전으로 트래픽을 이동하는 방법을 제어할 수 있다.
- Request Routing
  - 여러 버전의 마이크로서비스로 동적으로 라우팅하는 방법을 확인할 수 있다.
- Fault Injection
  - application 의 복원력을 테스트하기 위해서 결함을 주입할 수 있다.
- Circuit Breaking
  - istio는 Connection pool 과   Load balancing pool 기반의 circuit breaking 기능을 제공한다.







# 4. Class3: ArgoCD ( [가이드 문서 보기](./argocd/argocd.md) )  



## 1) GitOps

- GitOps 개요 / 원칙 / 배포전략



## 2) ArgoCD 개요

- Kubernetes를 위한 CD(Continuous Delivery)툴

  

## 3) 실습(개인PC)

- WSL에 ArgoCD 설치
- ArgoCD ingress 설정
- ArgoCD CLI 설정



## 4) 실습(KT Cloud)

- ArgoCD Project 구성(개인 NS에 userlist 배포)
- App 생성(ArgoCD UI에서)
- App 생성(ArgoCD CLI 이용)
- Deploy (Sync) 및 접속확인
- Git repo와의 Sync 이해 (Scale Out 적용) 





# 별첨. KT Cloud Setup ( [가이드 문서 보기](./ktcloud-setup/ktcloud-setup.md) )  

## 1) 서버 생성

- k3s Cluster 용도 VM 생성
- k3s 설치
- user 생성

## 2) Istio 셋팅

- helm 설치
- Istio 설치
- Monitoring 설치
  - Prometheus / Grafana / Kiali / Jeager 설치

## 3) ArgoCD 셋팅

- ArgoCD 설치
- ArgoCD CLI 설치

