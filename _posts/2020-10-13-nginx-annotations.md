---
title: "NGINX Annotations #2"
date: 2020-10-13 13:46:00 +0900
categories: kubernetes
---

### Server-side HTTPS enforcement through redirect
기본적으로 컨트롤러는 ingress에 대해 TLS가 활성화 된 경우 HTTPS로 리다이렉션 (**308**)을 합니다. 이 동작은 전역적으로 비활성화하려면 NGONX ConfigMap에서 `ssl-redirect: "false"` 를 사용합니다.

특정 ingress 리소스에 대해 이 기능을 구성하려면, `nginx.ingress.kubernetes.io/ssl-redirect: "false"` 어노테이션을 리소스에 사용합니다.

* Client --HTTP--> LB (Do not SSL offloading) --HTTP--> Nginx --HTTP--> Server 

* Client --HTTPS--> LB (Do not SSL offloading) --HTTPS--> Nginx --HTTPS--> Server 
* Client --HTTPS--> LB (Do SSL offloading) --HTTP--> Nginx --HTTP--> Server 

클러스터 외부 (예: AWS ELB)에서 SSL offloading을 사용하는 경우 사용 가능한 TLS 인증서가 없는 경우에도 HTTPS로 리다이렉션을 적용하는 것이 유용할 수 있습니다. 이는 리소스에서 `nginx.ingress.kubernetes.io/force-ssl-redirect: "true"` 주석을 사용하여 수행 할 수 있습니다.

* Client --HTTPS--> LB --HTTP--> Nginx --HTTPS--> Server 
