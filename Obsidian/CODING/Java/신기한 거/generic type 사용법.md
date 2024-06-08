
```java
public static <P extends Pair<K,V>, K , V> V getValue(P p, K k) {
    if (p.getKey() == k) {
        return p.getValue();
    } else {
        return null;
	    }
    }
```

## 제너릭 타입
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
## 리턴 타입
return type으로 V가 사용되고 parameter로 P와 K가 사용되는 것을 알 수 있다.

## 전체 코드

```java
public class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
}

public class Main {
    public static <P extends Pair<K, V>, K, V> V getValue(P p, K k) {
        if (p.getKey().equals(k)) {  // 수정: 객체 비교는 equals 메서드를 사용
            return p.getValue();
        } else {
            return null;
        }
    }

    public static void main(String[] args) {
        Pair<String, Integer> pair = new Pair<>("key", 100);
        Integer value = getValue(pair, "key");
        System.out.println(value);  // 출력: 100
    }
}
```
