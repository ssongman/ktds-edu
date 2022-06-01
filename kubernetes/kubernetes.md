# < 1교시: kubernetes 맛보기 >





[TOC]







# 1. Kubernetes 란 무엇인가?



참조링크: https://kubernetes.io/ko/docs/concepts/overview/components/

## 1) 개요

쿠버네티스는 컨테이너화된 워크로드와 서비스를 관리하기 위한 이식성이 있고, 확장가능한 오픈소스 플랫폼이다. 쿠버네티스는 선언적 구성과 자동화를 모두 용이하게 해준다. 쿠버네티스는 크고, 빠르게 성장하는 생태계를 가지고 있다. 쿠버네티스 서비스, 기술 지원 및 도구는 어디서나 쉽게 이용할 수 있다.

쿠버네티스란 명칭은 키잡이(helmsman)나 파일럿을 뜻하는 그리스어에서 유래했다. K8s라는 표기는 "K"와 "s"와 그 사이에 있는 8글자를 나타내는 약식 표기이다. 구글이 2014년에 쿠버네티스 프로젝트를 오픈소스화했다. 쿠버네티스는 프로덕션 워크로드를 대규모로 운영하는 [15년 이상의 구글 경험](https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/)과 커뮤니티의 최고의 아이디어와 적용 사례가 결합되어 있다.





## 2) 이전에는?





![배포 혁명](https://d33wubrfki0l68.cloudfront.net/26a177ede4d7b032362289c6fccd448fc4a91174/eb693/images/docs/container_evolution.svg)



![배포 혁명](kubernetes.assets/container_evolution.svg+xml)















**전통적인 배포 시대:** 초기 조직은 애플리케이션을 물리 서버에서 실행했었다. 한 물리 서버에서 여러 애플리케이션의 리소스 한계를 정의할 방법이 없었기에, 리소스 할당의 문제가 발생했다. 예를 들어 물리 서버 하나에서 여러 애플리케이션을 실행하면, 리소스 전부를 차지하는 애플리케이션 인스턴스가 있을 수 있고, 결과적으로는 다른 애플리케이션의 성능이 저하될 수 있었다. 이에 대한 해결책은 서로 다른 여러 물리 서버에서 각 애플리케이션을 실행하는 것이 있다. 그러나 이는 리소스가 충분히 활용되지 않는다는 점에서 확장 가능하지 않았으므로, 물리 서버를 많이 유지하기 위해서 조직에게 많은 비용이 들었다.

**가상화된 배포 시대:** 그 해결책으로 가상화가 도입되었다. 이는 단일 물리 서버의 CPU에서 여러 가상 시스템 (VM)을 실행할 수 있게 한다. 가상화를 사용하면 VM간에 애플리케이션을 격리하고 애플리케이션의 정보를 다른 애플리케이션에서 자유롭게 액세스 할 수 없으므로, 일정 수준의 보안성을 제공할 수 있다.

가상화를 사용하면 물리 서버에서 리소스를 보다 효율적으로 활용할 수 있으며, 쉽게 애플리케이션을 추가하거나 업데이트할 수 있고 하드웨어 비용을 절감할 수 있어 더 나은 확장성을 제공한다. 가상화를 통해 일련의 물리 리소스를 폐기 가능한(disposable) 가상 머신으로 구성된 클러스터로 만들 수 있다.

각 VM은 가상화된 하드웨어 상에서 자체 운영체제를 포함한 모든 구성 요소를 실행하는 하나의 완전한 머신이다.

**컨테이너 개발 시대:** 컨테이너는 VM과 유사하지만 격리 속성을 완화하여 애플리케이션 간에 운영체제(OS)를 공유한다. 그러므로 컨테이너는 가볍다고 여겨진다. VM과 마찬가지로 컨테이너에는 자체 파일 시스템, CPU 점유율, 메모리, 프로세스 공간 등이 있다. 기본 인프라와의 종속성을 끊었기 때문에, 클라우드나 OS 배포본에 모두 이식할 수 있다.

컨테이너는 다음과 같은 추가적인 혜택을 제공하기 때문에 인기가 있다.

- 기민한 애플리케이션 생성과 배포: VM 이미지를 사용하는 것에 비해 컨테이너 이미지 생성이 보다 쉽고 효율적임.
- 지속적인 개발, 통합 및 배포: 안정적이고 주기적으로 컨테이너 이미지를 빌드해서 배포할 수 있고 (이미지의 불변성 덕에) 빠르고 효율적으로 롤백할 수 있다.
- 개발과 운영의 관심사 분리: 배포 시점이 아닌 빌드/릴리스 시점에 애플리케이션 컨테이너 이미지를 만들기 때문에, 애플리케이션이 인프라스트럭처에서 분리된다.
- 가시성(observability): OS 수준의 정보와 메트릭에 머무르지 않고, 애플리케이션의 헬스와 그 밖의 시그널을 볼 수 있다.
- 개발, 테스팅 및 운영 환경에 걸친 일관성: 랩탑에서도 클라우드에서와 동일하게 구동된다.
- 클라우드 및 OS 배포판 간 이식성: Ubuntu, RHEL, CoreOS, 온-프레미스, 주요 퍼블릭 클라우드와 어디에서든 구동된다.
- 애플리케이션 중심 관리: 가상 하드웨어 상에서 OS를 실행하는 수준에서 논리적인 리소스를 사용하는 OS 상에서 애플리케이션을 실행하는 수준으로 추상화 수준이 높아진다.
- 느슨하게 커플되고, 분산되고, 유연하며, 자유로운 마이크로서비스: 애플리케이션은 단일 목적의 머신에서 모놀리식 스택으로 구동되지 않고 보다 작고 독립적인 단위로 쪼개져서 동적으로 배포되고 관리될 수 있다.
- 리소스 격리: 애플리케이션 성능을 예측할 수 있다.
- 자원 사용량: 리소스 사용량: 고효율 고집적





## 3) 왜 k8s 가 필요한가?



- **서비스 디스커버리와 로드 밸런싱** 쿠버네티스는 DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출할 수 있다. 컨테이너에 대한 트래픽이 많으면, 쿠버네티스는 네트워크 트래픽을 로드밸런싱하고 배포하여 배포가 안정적으로 이루어질 수 있다.
- **스토리지 오케스트레이션** 쿠버네티스를 사용하면 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소 시스템을 자동으로 탑재 할 수 있다.
- **자동화된 롤아웃과 롤백** 쿠버네티스를 사용하여 배포된 컨테이너의 원하는 상태를 서술할 수 있으며 현재 상태를 원하는 상태로 설정한 속도에 따라 변경할 수 있다. 예를 들어 쿠버네티스를 자동화해서 배포용 새 컨테이너를 만들고, 기존 컨테이너를 제거하고, 모든 리소스를 새 컨테이너에 적용할 수 있다.
- **자동화된 빈 패킹(bin packing)** 컨테이너화된 작업을 실행하는데 사용할 수 있는 쿠버네티스 클러스터 노드를 제공한다. 각 컨테이너가 필요로 하는 CPU와 메모리(RAM)를 쿠버네티스에게 지시한다. 쿠버네티스는 컨테이너를 노드에 맞추어서 리소스를 가장 잘 사용할 수 있도록 해준다.
- **자동화된 복구(self-healing)** 쿠버네티스는 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체하며, '사용자 정의 상태 검사'에 응답하지 않는 컨테이너를 죽이고, 서비스 준비가 끝날 때까지 그러한 과정을 클라이언트에 보여주지 않는다.
- **시크릿과 구성 관리** 쿠버네티스를 사용하면 암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리 할 수 있다. 컨테이너 이미지를 재구성하지 않고 스택 구성에 시크릿을 노출하지 않고도 시크릿 및 애플리케이션 구성을 배포 및 업데이트 할 수 있다.







# 2. 실습 환경 설명



## 1) mobaxterm

KT cloud 서버에 ssh 접근을 위한 터미널이 필요하다. 

다양한 터미널(putty 등)이 있지만 본 실습에서는 mobax term 이라는 free 버젼 솔루션을 사용한다.

- mobaxterm 실행

![image-20220601194018844](kubernetes.assets/image-20220601194018844.png)



## 2) wsl 

k3s, istio, argocd 설치는 Cluster 당 한번만 가능하다. 그러므로 이러한 설치실습은 본인 PC 에 wsl 에서 진행할 예정이다.

본인 PC 에 WSL이 설치되어 있는지 확인하자.



### (1) 확인 하는 방법

command 창에서 wsl 명령으로 설치여부를 확인 할 수 있다.

```sh
cmd > wsl -l -v 
```



![image-20220601193023175](kubernetes.assets/image-20220601193023175.png)



### (2) 실행하는 방법

실행하는 방법은 아래와 같이 다양하다. 본인이 편한 방법을 선택하자.

- cmd 창에서 바로실행
  - 위 command 창에서 wsl 명령을 입력하면 바로 default linux 가 실행된다.

![image-20220601193219422](kubernetes.assets/image-20220601193219422.png)



- winterm 으로 실행하는 방법
  - winterm 실행
    - 위 화면과 동일

- mobaxterm 에서 실행
  - session > WSL 실행

![image-20220601193859958](kubernetes.assets/image-20220601193859958.png)





## 3) docker desktop 확인

Container 와 kubernetes 의 차이를 이해하기 위해서 간단한 container 배포 테스트를 진행할 계획이다.



### (1) docker destktop 확인

우측 하단  docker desktop  아이콘에서 우클릭후 아래 그림 처럼 Docker Desktop is running 확인

![image-20220601192354841](kubernetes.assets/image-20220601192354841.png)



### (2) docker daemon 확인

docker 가 실행가능 곳에서 아래와 같이 version 을 확인하자.

```sh
$ docker version
Client:
 Version:           20.10.7
 API version:       1.41
 Go version:        go1.13.8
 Git commit:        20.10.7-0ubuntu5~20.04.2
 Built:             Mon Nov  1 00:34:17 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Desktop
 Engine:
  Version:          20.10.14
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.15
  Git commit:       87a90dc
  Built:            Thu Mar 24 01:46:14 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.5.11
  GitCommit:        3df54a852345ae127d1fa3092b95168e4a88e2f8
 runc:
  Version:          1.0.3
  GitCommit:        v1.0.3-0-gf46b6ba
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
  
```

Server version 을 확인할 수 있다면 정상 설치되었다고 볼 수 있다.







## 4) KT Cloud 서버

개인별 계정과 개인별 Namespace 에서 다양한 실습 진행을 위해서 서버 접근이 필요하다.



### (1) KT Cloud 설명

KT Cloud에 VM 서버 하나를 생성하게 되면 다음과 같은 구조가 된다.



![img](kubernetes.assets/010103012.png)

- vm 설명

  - 공인IP는 외부에서 접근을 할 수 있는 IP

  - 사설IP는 외부에서 접근은 못하나, 같은 서브넷 내에서 사용할 수 있는 IP
  - 외부에서 VM에 접근을 하기 위해서는 가상라우터에서 포트포워딩 작업이 필요하다.

- 가상라우터 (Virtual Router)

  - 사용자만 접근할 수 있는 서브넷과 외부의 관문(게이트웨이) 및 라우터 역할을 하는 가상 서버이다.

  - 한 계정의 한 zone에서 최초 VM을 생성하게 되면 자동으로 생성된다.

  - 기본으로 제공되어 과금이 되지 않으며, 사용자가 콘트롤 할 수 없다.

  - 하나의 공인IP가 기본으로 부여되며, 추가 공인IP를 할당할 수 있다.

- 포트포워딩

  - 가상라우터에서 외부에서 접근가능한 공인IP를 내부의 사설IP로 연결(포워딩) 해주는 작업이다.

  - 공인IP:공인 포트 <-> 사설IP:사설 포트 와 1:1 매핑이 기본이며, StaticNAT를 이용해 공인IP <-> 사설IP IP간의 매핑도 가능하다.



### (2) terminal (Mobaxterm) 실행

- 메뉴 : session > SSH 

- Romote host : 211.254.212.105
- User : user01  (개인별 계정)
- Port : 10022
- password : 별도 통지



![image-20220601194227476](kubernetes.assets/image-20220601194227476.png)





### (3) 개인별 환경설정

테스트를 위해서 github 자료를 받아 놓자.

```sh
$ mkdir ~/githubrepo

$ cd ~/githubrepo

$ git clone github.com/ssongman/ds-edu

$ cd ~/githubrepo/ds-edu
```





# 3. Docker 실습

docker Container 를 활용한 실습을 통해서 얼마나 효율적인지, 한계가 무엇인지, kubernetes 의 차이가 무엇인지를 알아보자.



## 1) sample app 실행

sample app 인 userlist 를 실행해 보자.

```sh
$ docker run -d --name userlist1 -p 8181:8181 ssongman/userlist:v1

$ curl http://localhost:8181/


$ curl http://localhost:8181/users/1
{"id":1,"name":"Ivory Leffler","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl http://localhost:8181/users/2
{"id":2,"name":"Albertha Schumm PhD","gender":"F","image":"/assets/image/cat2.jpg"}

```



크로브라우저에서 아래 주소로 접속 시도해 보자.

```sh
http://localhost:8181/ 

http://localhost:8181/users/1

http://localhost:8181/users/2
```

![image-20220601202716907](kubernetes.assets/image-20220601202716907.png)



Application 하나를 간단히 배포하였다. 

하지만 부하가 너무 많아 한개의 container 만으로는 부족한 상황이다.

Scale Out 이 필요한 상황이다.  어떻게 해결할 것인가??

동일한 이미지를 이용해서 한개 실행해보자.

```sh
$ docker run -d --name userlist2 -p 8182:8181 ssongman/userlist:v1

$ curl http://localhost:8182/users/1
{"id":1,"name":"Sherman Rath","gender":"F","image":"/assets/image/cat1.jpg"}
```

userlist1 번은 8181 이며 새롭게 실행한 2번째 app 은 8182 로 구분하여 실행하였다.



이전에 실행 userlist1 을 다시 확인해보자.

```sh
$ curl http://localhost:8181/users/1
{"id":1,"name":"Ivory Leffler","gender":"F","image":"/assets/image/cat1.jpg"}
```

동일한 uri 인 users/1 을 호출했지만 접근 port 번호가 틀려서 서로다른 값이 호출되었다.

userlist app 은 실행될때 10명의 사용자가 난수로 생성되도록 개발된 테스트용 app이다.



이렇게 두개의 App 을 실행되었다.  Client 가 두개의 App에 어떻게 접근해야 할까? 또한 부하분산을 어떻게 할까?

이런 문제를 해결하기 위해서는 load balancer 역할 수행하는 또다른 app 이 필요하다.



아래 그림을 살펴보자.



![Blue Green Architecture](kubernetes.assets/BG_using_haproxy.png)

load balancer 역할을 수행할 haproxy 를 Application 앞단에 두고 client 가 이를 바라보게 하였다. 충분히 부하분산 역할 수행할 수 있다.

하지만 haporxy container 를 별도로 관리해야 하고 application(userlist) 이 추가될때마다 haproxy 의 config 을 재구성해야 한다.

- haproxy container 내의 config file 설정

```sh
frontend testweb-front
    bind *:8180
    default_backend testweb-backend
    mode tcp
    option tcplog

backend testweb-backend
    balance roundrobin
    mode tcp
    server w1 userlist1:8181 check
    server w2 userlist2:8181 check
```



결국 Container 기반의 시스템 구성은 아래와 같이 결론 내릴 수 있다.



- 결론

  - 장점

    - 가상머신과 비교하여 컨테이너 생성이 쉽고 효율적

    - 컨테이너 이미지를 이용한 배포와 롤백이 간단

    - 언어나 프레임워크에 상관없이 애플리케이션을 동일한 방식으로 관리

    - 개발, 테스팅, 운영 환경을 물론 로컬 피시와 클라우드까지 동일한 환경을 구축

    - 특정 클라우드 벤더에 종속적이지 않음

  - 한계점
    - 서버 컨테이너 수가 점점 증가하게되면 관리가 힘들다는 문제가 발생한다.
    - 뭔가 다른 방법이 필요하다.
  - 솔루션
    - 이런 한계점을 극복하기 위해서 kubernetes 가 필요하다.



## 2) clean up

```sh
$ docker rm -f userlist1 userlist2
userlist1
userlist2
```







# 4. k3s 실습(개인PC)

## 1) wsl 에 k3s 설치

### (1) master node - stand alone

- k3s install

```sh
## root 권한으로 실행
$ sudo curl -sfL https://get.k3s.io | sh -

[INFO]  Finding release for channel stable
[INFO]  Using v1.23.6+k3s1 as release
…
[INFO]  systemd: Starting k3s   <-- 마지막 성공 로그


```



- 확인

```sh
$ k3s kubectl version
Client Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.23.6+k3s1", GitCommit:"418c3fa858b69b12b9cefbcff0526f666a6236b9", GitTreeState:"clean", BuildDate:"2022-04-28T22:16:18Z", GoVersion:"go1.17.5", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.23.6+k3s1", GitCommit:"418c3fa858b69b12b9cefbcff0526f666a6236b9", GitTreeState:"clean", BuildDate:"2022-04-28T22:16:18Z", GoVersion:"go1.17.5", Compiler:"gc", Platform:"linux/amd64"}

```

Client 와 Server Version 이 각각 보인다면 kubernetes cluster 에 연결이 잘 된 것이다.



### (2) kubeconfig 설정

local 에서 직접 kubctl 명령 실행을 위해서는 ~/.kube/config 에 연결정보가 설정되어야 한다.

현재는 /etc/rancher/k3s/k3s.yaml 에 정보가 존재하므로 이를 복사한다. 또한 모든 사용자가 읽을 수 있도록 권한을 부여 한다.

```sh
## root 권한으로 실행
## kubeconfig
$ mkdir -p ~/.kube
$ sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config


# 모든사용자에게 읽기 권한 부여
$ sudo chmod +r /etc/rancher/k3s/k3s.yaml ~/.kube/config

## 확인
## user 권한으로도 사용 가능
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.23.6+k3s1", GitCommit:"418c3fa858b69b12b9cefbcff0526f666a6236b9", GitTreeState:"clean", BuildDate:"2022-04-28T22:16:18Z", GoVersion:"go1.17.5", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.23.6+k3s1", GitCommit:"418c3fa858b69b12b9cefbcff0526f666a6236b9", GitTreeState:"clean", BuildDate:"2022-04-28T22:16:18Z", GoVersion:"go1.17.5", Compiler:"gc", Platform:"linux/amd64"}

```

이제 root 권한자가 아닌 다른 사용자도 kubectl 명령을 사용할 수 있다.





### (3) alias 정의

```sh
$ cat > ~/env
alias k='kubectl'
alias kk='kubectl -n kube-system'
alias ks='k -n song'
alias ka='k -n argocd'
alias kar='k -n argo-rollouts'
alias ki='k -n istio-system'
alias kb='k -n bookinfo'
alias kii='k -n istio-ingress'
alias kka='k -n kafka'

## alias 를 적용하려면 source 명령 수행
$ source ~/env
```

kubectl 명령과 각종 namespace 를 매번 입력하기가 번거롭다면 위와 같이 alias 를 정의후 사용할 수 있으니 참고 하자.

적용하려면 source 명령을 이용한다.







## 2) sample app deploy

### (1) namespace



```sh
## kubectl create ns [namespace_name]

$ kubectl create ns song

```



### (2) deployment

- yaml 확인

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: userlist
  labels:
    app: userlist
spec:
  replicas: 1
  selector:
    matchLabels:
      app: userlist
  template:
    metadata:
      labels:
        app: userlist
    spec:
      containers:
      - name: userlist
        image: ssongman/userlist:v1
        ports:
        - containerPort: 8181

```



- userlist deployment 생성

```sh
$ kubectl -n song create -f 11.userlist-deployment.yaml

$ kubectl -n song get pod
NAME                       READY   STATUS              RESTARTS   AGE
userlist-c78d76c78-52s27   0/1     ContainerCreating   0          5s


# 시간이 지나면 아래처럼 정상 기동됨

$ kubectl -n song get pod
NAME                       READY   STATUS    RESTARTS   AGE
userlist-c78d76c78-52s27   1/1     Running   0          112s

```



- pod 내에서 확인

```sh
$ kubectl -n song exec -it userlist-c78d76c78-52s27 -- bash


root@userlist-c78d76c78-52s27:/usr/src/app$ curl localhost:8181
HTTP/1.1 200
Content-Type: text/html;charset=UTF-8
Content-Language: en
Transfer-Encoding: chunked
Date: Wed, 01 Jun 2022 07:34:49 GMT

<!DOCTYPE html>

<html>
<head>
        <title>UMS - User List</title>
        <meta charset="utf-8" />
...

# 200 OK 로 정상


$ curl localhost:8181/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}root@userlist-c78d76c78-52s27:/usr/src/app#


```







### (3) curltest(test 목적 pod)

cat > 10.curltest.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: curltest
  labels:
    app: curltest
spec:
  replicas: 1
  selector:
    matchLabels:
      app: curltest
  template:
    metadata:
      labels:
        app: curltest
    spec:
      containers:
      - name: main
        image: curlimages/curl
        command: ["sleep", "365d"]
```



- 확인

```sh
$ kubectl -n song create -f 10.curltest.yaml


$ kubectl -n song get pod
NAME                        READY   STATUS        RESTARTS   AGE
userlist-c78d76c78-52s27    1/1     Running       0          21m
curltest-564b75669d-gsfnb   1/1     Running       0          16s


$ kubectl -n song get pod -o wide
NAME                        READY   STATUS        RESTARTS   AGE   IP           NODE              NOMINATED NODE   READINESS GATES
userlist-c78d76c78-52s27    1/1     Running       0          21m   10.42.0.9    desktop-msrerbm   <none>           <none>
curltest-564b75669d-gsfnb   1/1     Running       0          38s   10.42.0.11   desktop-msrerbm   <none>           <none>

```



- curltest pod 내에서 테스트

```sh

$ kubectl -n song exec -it curltest-564b75669d-gsfnb -- sh

$ curl 10.42.0.9:8181/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl 10.42.0.9:8181/users/2
{"id":2,"name":"Jaida Cartwright","gender":"F","image":"/assets/image/cat2.jpg"}/

```



- local 에서 실행

```sh
$ kubectl -n song exec -it curltest-564b75669d-gsfnb -- curl 10.42.0.9:8181/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

$ kubectl -n song exec -it curltest-564b75669d-gsfnb -- curl 10.42.0.9:8181/users/2
{"id":2,"name":"Jaida Cartwright","gender":"F","image":"/assets/image/cat2.jpg"}/

```



curltest pod 내에서 수행한 결과가 동일함.

이유 설명....



하지만 userlist pod 가 2개 이상일때 어떻게 주소를 찾아야 하며 어떻게 접근해야 하나???

그 솔루션이 바로 kubernetes service 라는 객체 이다.





### (3) service



- service 생성

```yaml
$ cat > 12.userlist-svc.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: userlist-svc
spec:
  selector:
    app: userlist
  ports:
  - name: http
    protocol: TCP
    port: 80
    targetPort: 8181
  type: ClusterIP
---

```



```sh
$ kubectl -n song create -f 12.userlist-svc.yaml
service/userlist-svc created


```



- curltest pod 내에서 테스트

```sh
$ kubectl -n song get pod -o wide
NAME                        READY   STATUS    RESTARTS   AGE   IP           NODE              NOMINATED NODE   READINESS GATES
userlist-c78d76c78-52s27    1/1     Running   0          77m   10.42.0.9    desktop-msrerbm   <none>           <none>
curltest-564b75669d-gsfnb   1/1     Running   0          56m   10.42.0.11   desktop-msrerbm   <none>           <none>

$ kubectl -n song exec -it curltest-564b75669d-gsfnb -- sh

# pod ip 로 call
$ curl 10.42.0.9:8181/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

# svc name으로 call
$ curl userlist-svc/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

# svc name 의 ip 식별
$ ping userlist-svc
PING userlist-svc (10.43.17.249): 56 data bytes

# svc ip로 call
$ curl 10.43.17.249/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

```



위 부분을 반드시 이해하기 바란다.  

이해 해야할 주요 포인트를 정리하자면...

- 여러가지 주소 형태로 call 을 했지만 모두 같은 값이 리턴되었다.
- pod ip 로 직접 접근할때는 8181 port  로 접근한다.
- svc name 이나 svc ip 로 접근할때는 80 port 로 접근한다.
- svc name 으로 call 이 가능하다.





### (4) Scale Out



```sh
$ ks get deploy
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
userlist   1/1     1            1           82m
curltest   1/1     1            1           61m

$ ks edit deploy userlist
```



```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  creationTimestamp: "2022-06-01T07:31:22Z"
  generation: 1
  labels:
    app: userlist
  name: userlist
  namespace: song
  resourceVersion: "2738"
  uid: a5548d35-3df2-4602-b080-b2396472c0e8
spec:
  progressDeadlineSeconds: 600
  replicas: 1                      <--- 3으로 수정한다.
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: userlist
      ....
```



```sh
$ ks get pod
NAME                        READY   STATUS    RESTARTS   AGE
userlist-c78d76c78-52s27    1/1     Running   0          83m
curltest-564b75669d-gsfnb   1/1     Running   0          63m
userlist-c78d76c78-wq9rw    1/1     Running   0          6s
userlist-c78d76c78-dcjph    1/1     Running   0          6s
```

너무나 쉽게 replicas 3 으로 scale out 이 되었다.



- curltest pod 내에서 테스트

```sh

$ kubectl -n song exec -it curltest-564b75669d-gsfnb -- sh
ke Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

# svc name으로 call - 여러번 해보자.
$ curl userlist-svc/users/1
{"id":1,"name":"Neva Langworth","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl userlist-svc/users/1
{"id":1,"name":"Sophia Zboncak","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl userlist-svc/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl userlist-svc/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl userlist-svc/users/1
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl userlist-svc/users/1
{"id":1,"name":"Sophia Zboncak","gender":"F","image":"/assets/image/cat1.jpg"}

```

호출할때마다 응답하는 pod 가 서로 달라진다는 점을 알 수 있다.



아래와 같이 1초에 한번씩 call 하도록 명령을 실행해보자.  더욱더 확실히 알수 있을 것이다.

```sh
$ while true; do curl userlist-svc/users/1; sleep 1; echo; done

{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Sophia Zboncak","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Sophia Zboncak","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Sophia Zboncak","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Neva Langworth","gender":"F","image":"/assets/image/cat1.jpg"}
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}
...
```

3개의 pod 를 Round Robbin 방식으로 call 하는 모습을 볼수 있다.

위 실습을 통해서 kubernetes 가 service discovery 와 load balancer 를 얼마나 쉽게 설정해 주는지를 알 수 있다.



### (5) Round Robbin

Round Robin 방식은 클라이언트의 요청을 단순하게 들어온 순서대로 순환을 하여 로드밸런싱을 처리하는 방법이다.



![img](kubernetes.assets/06010103.png)



위 그림과 같이 back-end에 3개의 서버가 존재하는 경우 '서버 1' 부터 '서버 3' 까지 새로운 연결이 생길 떄 마다, 1-2-3-1-2...과 같이 순환을 하는 방식이며  응답 시간이 빠르고 구성이 단순하다는 점이 장점이 있다.



### (6) ingress 

인그레스는 클러스터 내의 서비스에 대한 외부 접근을 관리하는 API 오브젝트이며, 일반적으로 HTTP를 관리한다.

인그레스는 부하 분산, SSL 종료, 명칭 기반의 가상 호스팅을 제공할 수 있다.

인그레스는 클러스터 외부에서 클러스터 내부 서비스로 HTTP와 HTTPS 경로를 노출한다. 트래픽 라우팅은 인그레스 리소스에 정의된 규칙에 의해 컨트롤된다.

- ingress architecture

![image-20220601181111605](kubernetes.assets/image-20220601181111605.png)



위 인그레스는 반드시 인그레스 컨트롤러가 있어야 한다.  그 인그레스 컨트롤러는 클러스터별로 사용자가 설정할 수 있으며 보통 nginx, haproxy, traefik 등과 같이 proxy 처리가 가능한 오픈소스 tool 을 주로 사용한다.

예를들면, Openshift 의 경우 haproxy 로 구성된 route 라는 오브젝트를 제공한다. 

우리가 실습하고 있는 환경에는 어떤 ingress controller 가 설치되어 있는지 살펴보자.



```sh
$ kubectl -n kube-system get svc
NAME             TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)                      AGE
kube-dns         ClusterIP      10.43.0.10      <none>          53/UDP,53/TCP,9153/TCP       4h14m
metrics-server   ClusterIP      10.43.133.193   <none>          443/TCP                      4h14m
traefik          LoadBalancer   10.43.184.177   172.22.253.23   80:32423/TCP,443:32762/TCP   4h13m
```

kubernetes 관리영역 Namespace 인 kube-system 에서 service 를 살펴보았다.

traefik(https://traefik.io/) 이라는 요즘 뜨고 있는 proxy tool 을 사용하는 것을 알 수 있다.

또한 node port 가  32423  인것을 알 수 있다.  그러므로 클러스터 외부에서 접근할때는 해당 node port 로 접근이 가능하다.



그럼 실제로 ingress 를 선언하여 접근해보자.

- ingress yaml

```sh
cat > 15.userlist-ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: userlist-ingress
  annotations:
    kubernetes.io/ingress.class: "traefik"
spec:
  rules:
  - host: "userlist.songlab.co.kr"
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: userlist-svc
            port:
              number: 80
```



- 실행

```sh
$ ks create -f 15.userlist-ingress.yaml
ingress.networking.k8s.io/userlist-ingress created

$ ks get ingress
NAME               CLASS    HOSTS                    ADDRESS         PORTS   AGE
userlist-ingress   <none>   userlist.songlab.co.kr   172.22.253.23   80      21s

```





- local 에서 확인

```sh
$ curl http://localhost:32423/users/1 -H "Host:userlist.songlab.co.kr"
{"id":1,"name":"Sophia Zboncak","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl http://localhost:32423/users/1 -H "Host:userlist.songlab.co.kr"
{"id":1,"name":"Neva Langworth","gender":"F","image":"/assets/image/cat1.jpg"}

$ curl http://localhost:32423/users/1 -H "Host:userlist.songlab.co.kr"
{"id":1,"name":"Ms. Drake Murphy","gender":"F","image":"/assets/image/cat1.jpg"}


```

이제 userlist 에 접근할때 local 에서도 직접 접근할 수 있게 되었다. 위 service 테스트시 userlist 접근을 위해서는 cluster inner network 에 진입을 위해서 curltest pod 내에서 테스트를 진행했었다. 이제는 ingress 라는 오브젝가 외부와의 접근을 연결시켜주기 때문에 굳이 curltest pod 가 필요없으며 local 에서 직접 테스트 할 수 있다.



하지만 이 또한 완전환 모습은 아니다.  연결할때마다 node port 32423 를 붙여야 하는 불편함이 존재한다. 이런 불편을 해결하기 위해서 일반적으로 L4 라는 load balancer 를 둔다. 하만 지금환경은 개인 PC 이므로 이해만 하자.



- 참고
  - KTCloud 의 로드발란싱 개념 설명 : https://cloud.kt.com/portal/user-guide/network-loadbalancer-intro





# 5. K3s 실습(KT Cloud)

## 1) k3s 설치(참고)



### (1) master node - HA 구성

```sh
# master01에서
$ curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644 --cluster-init


# IP/ token 확인
$ cat /var/lib/rancher/k3s/server/node-token

K1019c3c05ec020248e5ebff9f8543bd167b7c76e22391b0d736d2a842814e9adeb::server:c5af856d2bb905e359a2f911815d71f5


# master02, 03 에서

$ export MASTER_TOKEN="K1019c3c05ec020248e5ebff9f8543bd167b7c76e22391b0d736d2a842814e9adeb::server:c5af856d2bb905e359a2f911815d71f5"
$ export MASTER_IP="172.27.0.138"


$ curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644 --server https://${MASTER_IP}:6443 --token ${MASTER_TOKEN}

…
[INFO]  systemd: Starting k3s-agent   ← 정상 로그



## istio setup 을 위한 k3s 설정
## traefik 을 deploy 하지 않는다. 
## istio 에서 별도 traefic 을 설치하는데 이때 기설치된 controller 가 있으면 충돌 발생함
curl -sfL https://get.k3s.io |INSTALL_K3S_EXEC="--no-deploy traefik" sh -


# uninstall
$ sh /usr/local/bin/k3s-killall.sh
  sh /usr/local/bin/k3s-uninstall.sh 


```



- worker node

```sh


$ export MASTER_TOKEN="K1019c3c05ec020248e5ebff9f8543bd167b7c76e22391b0d736d2a842814e9adeb::server:c5af856d2bb905e359a2f911815d71f5"

export MASTER_IP="172.27.0.138"


curl -sfL https://get.k3s.io | K3S_URL=https://${MASTER_IP}:6443 K3S_TOKEN=${MASTER_TOKEN} sh -

…
[INFO]  systemd: Starting k3s-agent   ← 나오면 정상




# < 수동방식 >

$ sudo k3s agent --server https://${MASTER_IP}:6443 --token ${NODE_TOKEN} &


## uninstall
$ sh /usr/local/bin/k3s-killall.sh
  sh /usr/local/bin/k3s-uninstall.sh

```



## 2) 개인 Namespace 확인



```sh
$ kubectl get ns
NAME              STATUS   AGE
default           Active   26m
kube-node-lease   Active   26m
kube-public       Active   26m
kube-system       Active   26m
user01            Active   111s
user02            Active   110s
user03            Active   110s


$ kubectl get ns user01
NAME     STATUS   AGE
user01   Active   2m4s


$ alias ku='kubectl -n user01'

$ ku get pod
No resources found in user01 namespace.

```





## 3) Sample app deploy



### (1) deployment

```sh

$ cd ~/githubrepo/ds-edu

kubectl -n user01 create -f ~/githubrepo/ds-edu/userlist/


```





### (2) service

### (3) ingress 

### (4) Scale Out



## 4) traffic 흐름 이해

### 












