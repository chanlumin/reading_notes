##  两个Key值相同，但不一定是同一个对象

  
```java
public class Main {
    public static void main(String[] args) {
        String key1 = "a";
        Map<String, Integer> map = new HashMap<>();
        map.put(key1, 123);

        String key2 = new String("a");
        map.get(key2); // 123

        System.out.println(key1 == key2); // false
        System.out.println(key1.equals(key2)); // true
    }
}


// 作为key的对象必须正确覆写equals()方法，相等的两个key实例调用equals()必须返回true；

// 作为key的对象还必须正确覆写hashCode()方法，且hashCode()方法要严格遵循以下规范：

// 如果两个对象相等，则两个对象的hashCode()必须相等；
// 如果两个对象不相等，则两个对象的hashCode()尽量不要相等。
// 即对应两个实例a和b：

// 如果a和b相等，那么a.equals(b)一定为true，则a.hashCode()必须等于b.hashCode()；
// 如果a和b不相等，那么a.equals(b)一定为false，则a.hashCode()和b.hashCode()尽量不要相等。
```


### hashCode
1. 两个对象不想等，两个对象的hashCode尽量不相等
2. 两个对象相等 两个对象的hashCode一定相等，


```java
public class Person {
    String firstName;
    String lastName;
    int age;

    @Override
    int hashCode() {
        int h = 0;
        h = 31 * h + firstName.hashCode();
        h = 31 * h + lastName.hashCode();
        h = 31 * h + age;
        return h;
    }
}

// 如果firstName和lastName为null的话 会抛出错误 
// 一般借助Objects.hash()来写hash

int hashCode() {
    return Objects.hash(firstName, lastName, age);
}
```


### hash冲突

1. 我们把不同的key具有相同的hashCode()的情况称之为哈希冲突。在冲突的时候，一种最简单的解决办法是用List存储hashCode()相同的key-value。显然，如果冲突的概率越大，这个List就越长，Map的get()方法效率就越低，这就是为什么要尽量满足条件二：

> 在hash冲突中, 解决方法就是在同一个Hash的位置用List存储，这样子hashCode一样的时候，就不会被覆盖了。




### 总结
要正确使用HashMap，作为key的类必须正确覆写equals()和hashCode()方法；

一个类如果覆写了equals()，就必须覆写hashCode()，并且覆写规则是：

如果equals()返回true，则hashCode()返回值必须相等；

如果equals()返回false，则hashCode()返回值尽量不要相等。

实现hashCode()方法可以通过Objects.hashCode()辅助方法实现。

