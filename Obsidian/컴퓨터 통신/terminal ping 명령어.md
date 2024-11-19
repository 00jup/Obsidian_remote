
```shell
sudo ping -l 1500 192.168.0.41
```

-c 옵션을 사용하면 개수 지정이 가능하다
```shell
sudo ping -c 1000 -l 1500 192.168.0.41
```

근데 -l 옵션이랑 -s 옵션이랑 뭐가 다르지

Linux ping 명령어의 -l과 -s 옵션:

-l: 패킷의 TTL(Time To Live) 값 설정

-s: 패킷의 크기(byte) 설정


```
    ~  sudo ping -c 100 -l 1500 -s 1500 192.168.0.41                  127 ✘  base   00:51:16 
Password:
PING 192.168.0.41 (192.168.0.41): 1500 data bytes
1508 bytes from 192.168.0.41: icmp_seq=0 ttl=64 time=0.364 ms
1508 bytes from 192.168.0.41: icmp_seq=1 ttl=64 time=0.286 ms
1508 bytes from 192.168.0.41: icmp_seq=2 ttl=64 time=0.306 ms
1508 bytes from 192.168.0.41: icmp_seq=3 ttl=64 time=0.336 ms
1508 bytes from 192.168.0.41: icmp_seq=4 ttl=64 time=0.346 ms
1508 bytes from 192.168.0.41: icmp_seq=5 ttl=64 time=0.363 ms
1508 bytes from 192.168.0.41: icmp_seq=6 ttl=64 time=0.371 ms
1508 bytes from 192.168.0.41: icmp_seq=7 ttl=64 time=0.427 ms
1508 bytes from 192.168.0.41: icmp_seq=8 ttl=64 time=0.409 ms
1508 bytes from 192.168.0.41: icmp_seq=9 ttl=64 time=0.392 ms
1508 bytes from 192.168.0.41: icmp_seq=10 ttl=64 time=0.291 ms
1508 bytes from 192.168.0.41: icmp_seq=11 ttl=64 time=0.254 ms
1508 bytes from 192.168.0.41: icmp_seq=12 ttl=64 time=0.259 ms
1508 bytes from 192.168.0.41: icmp_seq=13 ttl=64 time=0.266 ms
1508 bytes from 192.168.0.41: icmp_seq=14 ttl=64 time=0.321 ms
1508 bytes from 192.168.0.41: icmp_seq=15 ttl=64 time=0.318 ms
1508 bytes from 192.168.0.41: icmp_seq=16 ttl=64 time=0.271 ms
1508 bytes from 192.168.0.41: icmp_seq=17 ttl=64 time=0.309 ms
1508 bytes from 192.168.0.41: icmp_seq=18 ttl=64 time=0.312 ms
1508 bytes from 192.168.0.41: icmp_seq=19 ttl=64 time=0.325 ms
1508 bytes from 192.168.0.41: icmp_seq=20 ttl=64 time=0.354 ms
1508 bytes from 192.168.0.41: icmp_seq=21 ttl=64 time=0.361 ms
1508 bytes from 192.168.0.41: icmp_seq=22 ttl=64 time=0.330 ms
1508 bytes from 192.168.0.41: icmp_seq=23 ttl=64 time=0.310 ms
1508 bytes from 192.168.0.41: icmp_seq=24 ttl=64 time=0.326 ms
1508 bytes from 192.168.0.41: icmp_seq=25 ttl=64 time=0.265 ms
1508 bytes from 192.168.0.41: icmp_seq=26 ttl=64 time=0.234 ms
1508 bytes from 192.168.0.41: icmp_seq=27 ttl=64 time=0.135 ms
1508 bytes from 192.168.0.41: icmp_seq=28 ttl=64 time=0.110 ms
1508 bytes from 192.168.0.41: icmp_seq=29 ttl=64 time=0.323 ms
1508 bytes from 192.168.0.41: icmp_seq=30 ttl=64 time=0.265 ms
1508 bytes from 192.168.0.41: icmp_seq=31 ttl=64 time=0.284 ms
1508 bytes from 192.168.0.41: icmp_seq=32 ttl=64 time=0.318 ms
1508 bytes from 192.168.0.41: icmp_seq=33 ttl=64 time=0.339 ms
1508 bytes from 192.168.0.41: icmp_seq=34 ttl=64 time=0.376 ms
1508 bytes from 192.168.0.41: icmp_seq=35 ttl=64 time=0.396 ms
1508 bytes from 192.168.0.41: icmp_seq=36 ttl=64 time=0.414 ms
1508 bytes from 192.168.0.41: icmp_seq=37 ttl=64 time=0.456 ms
1508 bytes from 192.168.0.41: icmp_seq=38 ttl=64 time=0.476 ms
1508 bytes from 192.168.0.41: icmp_seq=39 ttl=64 time=0.511 ms
1508 bytes from 192.168.0.41: icmp_seq=40 ttl=64 time=0.527 ms
1508 bytes from 192.168.0.41: icmp_seq=86 ttl=64 time=0.281 ms
1508 bytes from 192.168.0.41: icmp_seq=88 ttl=64 time=0.288 ms
1508 bytes from 192.168.0.41: icmp_seq=89 ttl=64 time=0.286 ms
1508 bytes from 192.168.0.41: icmp_seq=90 ttl=64 time=0.280 ms
1508 bytes from 192.168.0.41: icmp_seq=91 ttl=64 time=0.273 ms
1508 bytes from 192.168.0.41: icmp_seq=92 ttl=64 time=0.305 ms
1508 bytes from 192.168.0.41: icmp_seq=93 ttl=64 time=0.300 ms
1508 bytes from 192.168.0.41: icmp_seq=94 ttl=64 time=0.285 ms
1508 bytes from 192.168.0.41: icmp_seq=95 ttl=64 time=0.279 ms
1508 bytes from 192.168.0.41: icmp_seq=96 ttl=64 time=0.274 ms
1508 bytes from 192.168.0.41: icmp_seq=97 ttl=64 time=0.278 ms
1508 bytes from 192.168.0.41: icmp_seq=98 ttl=64 time=0.262 ms
1508 bytes from 192.168.0.41: icmp_seq=99 ttl=64 time=0.256 ms
Request timeout for icmp_seq 98

--- 192.168.0.41 ping statistics ---
100 packets transmitted, 54 packets received, 46.0% packet loss
round-trip min/avg/max/stddev = 0.110/0.320/0.527/0.075 ms
```

```shell
ping -c 100 -l 1500  -s 2000 -D 192.168.0.41
```

단편화 확인을 위한 옵션처리

[[terminal ping option]]
