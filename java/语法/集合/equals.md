### 
```java
List<String> list = List.of("A", "B", "C");
System.out.println(list.contains("C")); // true
System.out.println(list.contains("X")); // false
System.out.println(list.indexOf("C")); // 2
System.out.println(list.indexOf("X")); // 


// new出来实例实际上是不一致的
List<String> list = List.of("A", "B", "C");
System.out.println(list.contains(new String("C"))); // true or false?
System.out.println(list.indexOf(new String("C"))); // 2 or -1?
//List内部并不是通过==判断两个元素是否相等，而是使用equals()方法判断两个元素是否相等，例如contains()方法可以实现如下：

public class ArrayList {
    Object[] elementData;
    public boolean contains(Object o) {
        for (int i = 0; i < size; i++) {
            if (o.equals(elementData[i])) {
                return true;
            }
        }
        return false;
    }
}


public boolean equals(Object o) {
    if (o instanceof Person) {
        Person p = (Person) o;
        return Objects.equals(this.name, p.name) && this.age == p.age;
    }
    return false;
}

public class Person {
    public String name;
    public int age;
}

```
1. equals()方法的正确编写方法：

先确定实例“相等”的逻辑，即哪些字段相等，就认为实例相等；
用instanceof判断传入的待比较的Object是不是当前类型，如果是，继续比较，否则，返回false；
对引用类型用Objects.equals()比较，对基本类型直接用==比较。
使用Objects.equals()比较两个引用类型是否相等的目的是省去了判断null的麻烦。两个引用类型都是null时它们也是相等的。

如果不调用List的contains()、indexOf()这些方法，那么放入的元素就不需要实现equals()方法。


reference: https://www.liaoxuefeng.com/wiki/1252599548343744/1265116446975264