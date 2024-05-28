
```java
public static <P extends Pair<K,V>, K , V> V getValue(P p, K k) {
    if (p.getKey() == k) {
        return p.getValue();
    } else {
        return null;
	    }
    }
```

여기서 `<P extends Pair<K,V>, K, V >`의 의미는 무엇일까?

제너릭 타입을 의미하는데 P가 Pair<K,V>, K, V 이렇