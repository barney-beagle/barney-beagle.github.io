---
title: "NGINX Annotations"
date: 2020-10-08 11:30:00 +0900
categories: kubernetes
---

### Custom max body size
NGINX에서 요청의 크기가 클라이언트 요청 본문의 최대 허용 크기를 초과하면 413 에러를 클라이언트로 반환합니다. 이 크기는 `client_max_body_size` 파라미터로 설정할 수 있습니다.

모든 Ingress 규칙에 대해 이 설정을 전역적으로 구성하려면 `proxy-body-size` 값을 NGINX ConfigMap에 설정합니다. Ingress 규칙에서 사용자 가 정의한 값을 사용하려면 다음 annotation을 정의합니다.
```
nginx.ingress.kubernetes.io/proxy-body-size: 1024m
```
`client_max_body_size` 파라미터는 **Content-Length** 요청 헤더 필드에 지정된 클라이언트 요청 본문의 최대 허용 크기를 설정합니다.
크기를 0으로 설정하면 클라이언트 요청 본문 크기를 확인하지 않습니다.

[kubernetes NGINX annotations]: https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-max-body-size
[NGINX client_max_body_size]: http://nginx.org/en/docs/http/ngx_http_core_module.html#client_max_body_size
