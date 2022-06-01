# < 2교시: Service Mesh >





# 1. helm 설치





## 2. istio 설치



```

cd ~/song/helm/

# 1. helm repo add

$ helm repo add istio https://istio-release.storage.googleapis.com/charts

← 오래 걸리네… 왜지??  기다리면 되긴 하네…


$ helm repo update



# 2. create ns
$ k create namespace istio-system


# 3. install ControlPlain 
$ helm install istio-base istio/base -n istio-system

← istio 설치를 위한 crd 설치

or fetch 받아서

$ helm -n istio-system install istio-base .


$ helm -n istio-system ls


# 4. install istiod
$ helm -n istio-system install istiod istio/istiod --wait  ← remote
$ helm -n istio-system install istiod .                    ← local(fetch 이후)


# 6. check

$ helm -n istio-system status istio-base
$ helm -n istio-system get all istio-base

$ helm -n istio-system status istiod
$ helm -n istio-system get all istiod

$ alias ki='k -n istio-system'
$ ki get all



# 7. clean up
$ helm -n istio-system delete istiod 
$ helm -n istio-system delete istio-base 

```

