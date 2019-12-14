# envoy docker deployment

~~~~
>vagrant up vg-envoy-01
$ sudo docker pull envoyproxy/envoy-dev:817b2e36689cbc9e32892fc53f253f8e6361d5dd

$ sudo docker image ls
REPOSITORY                 TAG                                        IMAGE ID            CREATED             SIZE
envoyproxy/envoy-dev       817b2e36689cbc9e32892fc53f253f8e6361d5dd   83b6bd0577e9        2 days ago          151MB

$ sudo  docker run --rm -d -p 10000:10000 envoyproxy/envoy-dev:817b2e36689cbc9e32892fc53f253f8e6361d5dd

$ sudo docker container ls
CONTAINER ID        IMAGE                                                           COMMAND                  CREATED             STATUS              PORTS                      NAMES
0818ab5f2704        envoyproxy/envoy-dev:817b2e36689cbc9e32892fc53f253f8e6361d5dd   "/docker-entrypoint.…"   5 minutes ago       Up 5 minutes        0.0.0.0:10000->10000/tcp   epic_driscoll

$ curl -v vg-envoy-01.local:10000
$ curl -v localhost:10000

A very minimal Envoy configuration that can be used to validate basic plain HTTP proxying is available in configs/google_com_proxy.v2.yaml.
https://github.com/envoyproxy/envoy/blob/74436a6303825e0a6873222efff591ea1001cf87/configs/google_com_proxy.v2.yaml

~~~~
~~~~
vagrant@vg-envoy-01:/vagrant$ cat /vagrant/envoy.yaml

vagrant@vg-envoy-01:~$ cd /vagrant
vagrant@vg-envoy-01:/vagrant$ sudo docker build -t envoy:v1 .
vagrant@vg-envoy-01:/vagrant$ sudo docker image ls
REPOSITORY             TAG                                        IMAGE ID            CREATED             SIZE
envoy                  v1                                         5528c0a59859        10 minutes ago      151MB
envoyproxy/envoy-dev   817b2e36689cbc9e32892fc53f253f8e6361d5dd   83b6bd0577e9        3 months ago        151MB

vagrant@vg-envoy-01:/vagrant$ sudo docker run -d --name envoy -p 9901:9901 -p 10000:10000 envoy:v1
554ecfb7ae2da78402c1bef2b3f20d32e2e3dd56f05bd62a7ef3a7f1ccd2868a
vagrant@vg-envoy-01:/vagrant$ curl -v localhost:10000
* Expire in 0 ms for 6 (transfer 0x5561f1bac5c0)
* Expire in 1 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 0 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 2 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 1 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 1 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 4 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 1 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 1 ms for 1 (transfer 0x5561f1bac5c0)
* Expire in 2 ms for 1 (transfer 0x5561f1bac5c0)
*   Trying ::1...
* TCP_NODELAY set
* Expire in 149997 ms for 3 (transfer 0x5561f1bac5c0)
* Expire in 200 ms for 4 (transfer 0x5561f1bac5c0)
* connect to ::1 port 10000 failed: Connection refused
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Expire in 149996 ms for 3 (transfer 0x5561f1bac5c0)
* connect to 127.0.0.1 port 10000 failed: Connection refused
* Failed to connect to localhost port 10000: Connection refused
* Closing connection 0
curl: (7) Failed to connect to localhost port 10000: Connection refused
~~~~
~~~~
Quick Start to Run Simple Example
https://www.envoyproxy.io/docs/envoy/latest/start/start
~~~~
