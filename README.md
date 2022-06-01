# ktds-edu
ktds Container 기반 istio, argocd 교육자료



# 서비스메쉬와 ArgoCD기반 CICD(6/13)





# 1. 커리큘럼



## 1) Class1: kubernetes - 2시간



1. kubernetes 이론교육
   1. 

2. k3s 실습(개인PC)
   1. wsl에 k3s 설치
   2. kubectl 명령 확인
   3. 개인 Namespace 생성 및 sample app(userlist) run
   4. ingress 접속 및 접속테스트
   5. Scale Out
3. K3s 실습(KT Cloud)
       1. 실습환경(KT Cloud) 설명
          1. 개인 계정 login 설명
       2. 개인 Namespace 에 userlist Run
       3. Ingress 설정 및 접속테스트
       4. Scale Out
          1. docker 와의 차이점
       5. traffic 흐름 이해
          1. Round Robbin
          2. Sticky Seession



## 2) Class2: ServiceMesh - 3시간



1. Istio 이론교육
   1. ServiceMesh 란?
   2. Istio Traffic 흐름 설명
   3. Istio 로 할 수 있는 것들 설명
2. 실습(개인PC)
   1. wsl에 istio 설치
   2. Sample app(userlist) istio sidecar inject
   3. ingress  / istio-ingress Gateway / VirtualService / Gateway 설정
3. 실습(KT Cloud)
   1. 개인 NS userlist 에 sidecar inject
   2. Ingress  / istio-ingress Gateway / VirtualService / Gateway 설정
   3. 접속테스트
   4. Kiali / Jaeger / Grafana (기 설치된 환경)
   5. Canary Test
   6. Circuit Breaker Test



## 3) Class3: ArgoCD - 3시간



1. ArgoCD 이론
2. 실습(개인PC)
   1. wsl 에 argocd 설치
   2. ArgoCD Project 구성(sample app)
   3. Sync 및 접속확인
3. 실습(KT Cloud)
   1. ArgoCD Project 구성(개인 NS에 userlist 배포)
      1. 동일Project 구성
   2. Sync 및 접속확인
   3. rgo-rollout 테스트
   4. app in apps pattern 테스트 ??







## backup



1. Class1: kubernetes 교육 - 2시간
   1. kubernetes 이론교육
   2. k3s 실습(개인PC)
          1. wsl에 k3s 설치
          2. kubectl 명령 확인
          3. 개인 Namespace 생성 및 sample app(userlist) run
          4. ingress 접속 및 접속테스트
          5. Scale Out
   3. K3s 실습(KT Cloud)
           1. 실습환경(KT Cloud) 설명
                 1. 개인 계정 login 설명
           2. 개인 Namespace 에 userlist Run
           3. Ingress 설정 및 접속테스트
           4. Scale Out
                 1. docker 와의 차이점
           5. traffic 흐름 이해
                 1. Round Robbin
                 2. Sticky Seession
2. Class2: ServiceMesh - 3시간
   1. Istio 이론교육
      1. ServiceMesh 란?
      2. Istio Traffic 흐름 설명
      3. Istio 로 할 수 있는 것들 설명
   2. 실습(개인PC)
      1. wsl에 istio 설치
      2. Sample app(userlist) istio sidecar inject
      3. ingress  / istio-ingress Gateway / VirtualService / Gateway 설정
   3. 실습(KT Cloud)
          1. 개인 NS userlist 에 sidecar inject
          2. Ingress  / istio-ingress Gateway / VirtualService / Gateway 설정
          3. 접속테스트
          4. Kiali / Jaeger / Grafana (기 설치된 환경)
          5. Canary Test
          6. Circuit Breaker Test
3. Class3: ArgoCD - 3시간
   1. ArgoCD 이론
   2. 실습(개인PC)
      1. wsl 에 argocd 설치
      2. ArgoCD Project 구성(sample app)
      3. Sync 및 접속확인
   3. 실습(KT Cloud)
      1. ArgoCD Project 구성(개인 NS에 userlist 배포)
         1. 동일Project 구성
      2. Sync 및 접속확인
      3. rgo-rollout 테스트
      4. app in apps pattern 테스트 ??



