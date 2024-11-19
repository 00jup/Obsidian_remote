
## DNS
```shell
dns contains "google"
```

""로 문자열을 인식한다.

## MAC (ether)
```shell
eth.addr == 9e:11:ef:24:90:a9 || eth.addr == 22:b2:35:70:3f:b9
```

```shell
eth.addr == 9e:11:ef:24:90:a9 eth.src == 22:b2:35:70:3f:b9 eth.dst == 9e:11:ef:24:90:a9
```

mac 주소 검색하는 방법

## IP
```shell
ip.src == 10.210.41.231 || ip.dst == 10.210.41.231
```

```shell
ip.src == 10.210.41.231 && ip.dst == 10.210.41.231
```