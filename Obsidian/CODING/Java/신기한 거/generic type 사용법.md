
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

제너릭 타입을 의미하는데 P는 Pair<K,V>을 통해서, K, V 이렇게 3가지가 될 수 있다는 의미이다.

그래서 함수를 살펴봤을 때

public static `<P extends Pair<K,V>`, `K` , `V`> `V` getValue(`P` p, `K` k) {
    if (p.getKey() == k) {
        return p.getValue();
    } else {
        return null;
	    }
    }

return type으로 V가 사용되고 parameter로 P와 K가 사용되는 것을 알 수 있다.