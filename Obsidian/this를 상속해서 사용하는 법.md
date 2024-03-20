```java
public class Laptop {  
    String model = "GalaxyBook";  
    int year = 2023;  
    Laptop(String model){  
        this.model = model;  
    }  
    Laptop(String model, int year){  
        this(model);  
        this.year= year;  
    }  
}
```

`오버로딩이 되기 때문에 할 수 있는 일임`

this(model)