
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