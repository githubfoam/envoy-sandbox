
# envoy sandbox

vagrant-envoy-01
~~~~
>vagrant up vagrant-envoy-01

>vagrant ssh agrant-envoy-01
[vagrant@vagrant-envoy-01 ~]$ envoy --version
envoy  version: a78311faf214bb9216f92407102b547b6fcd14a3/1.13.0-dev/clean-getenvoy-4bd7718-envoy/RELEASE/BoringSSL
[vagrant@vagrant-envoy-01 ~]$ getenvoy --version
getenvoy version 0.1.8

[vagrant@vagrant-envoy-01 ~]$ getenvoy run standard:1.11.1 -- --config-path ./basic-front-proxy.yaml

# shell window-2
>vagrant ssh agrant-envoy-01
[vagrant@vagrant-envoy-01 ~]$ curl -s -o /dev/null -vvv -H 'Host: google.com' localhost:15001
[vagrant@vagrant-envoy-01 ~]$  curl -vvv -H 'Host: google.com' localhost:15001
[vagrant@vagrant-envoy-01 ~]$  curl -s -o /dev/null -vvv -H 'Host: bing.com' localhost:15001
[vagrant@vagrant-envoy-01 ~]$  curl -vvv -H 'Host: bing.com' localhost:15001


# shell window-1 (monitoring)

[2019-12-13T23:39:12.069Z] "GET / HTTP/1.1" 200 - 0 13466 206 204 "-" "curl/7.61.1" "a1f4f13d-4df8-4a53-a19c-7906e766b9a5" "www.google.com" "216.58.212.4:80"
[2019-12-13T23:40:42.076Z] "GET / HTTP/1.1" 200 - 0 13511 216 211 "-" "curl/7.61.1" "6ecee04e-3382-432b-89b8-a58b1c6300cc" "www.google.com" "216.58.212.4:80"
[2019-12-13T23:43:13.317Z] "GET /curl HTTP/1.1" 404 - 0 1565 66 66 "-" "curl/7.61.1" "63e6ea7e-8dbc-4412-ae11-50c3665ac916" "www.google.com" "216.58.212.4:80"
[2019-12-13T23:43:14.748Z] "GET / HTTP/1.1" 200 - 0 96626 275 222 "-" "curl/7.61.1" "a9f80fd9-5139-4c37-baa8-dfb249a59092" "www.bing.com" "13.107.21.200:80"
[2019-12-13T23:43:43.635Z] "GET / HTTP/1.1" 200 - 0 96626 251 190 "-" "curl/7.61.1" "f3340e97-08a8-40b1-a103-3e1be11c3a79" "www.bing.com" "13.107.21.200:80"

~~~~
~~~~
<https://www.envoyproxy.io/community>
<https://www.getenvoy.io/>
GetEnvoy CLI
https://www.getenvoy.io/install/cli/
Standard Envoy Binary
https://www.getenvoy.io/install/envoy/
When we hit Envoy with the host header google.com it will proxy our request to www.google.com and when we hit Envoy with the host header bing.com it will proxy our request to www.bing.com
<https://www.getenvoy.io/tutorials/front-proxy/>
~~~~
