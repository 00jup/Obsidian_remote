
```java
String a = new String("test");
String b = new String("test");

// == 사용
if (a == b) {
    // 이 조건은 거짓이다. a와 b는 같은 내용을 가지고 있지만, 다른 메모리 주소를 가리킨다.
}

// equals 사용
if (a.equals(b)) {
    // 이 조건은 참이다. a와 b의 내용이 같기 때문이다.
}
```


```java
for(int j =0; j<i; j++){  
    if (new_account[j].account_num.equals(account_num)){  
        new_account[j].draw(total_money);  
        System.out.println(new_account[j].total_money);  
        break;  
    }  
}
```

나도 여기서 비교할 때 
>==을 사용했다. 이건 나중에 알아도 못 찾을 수 있으니 주의하자!
