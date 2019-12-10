# 父类通配符可以接受当前和父类型的Pair 

```java

void set(Pair<? super Integer> p, Integer first, Integer last) {
    p.setFirst(first);
    p.setLast(last);
}


public class Main {
    public static void main(String[] args) {
        Pair<Number> p1 = new Pair<>(12.3, 4.56);
        Pair<Integer> p2 = new Pair<>(123, 456);
        setSame(p1, 100);
        setSame(p2, 200);
        System.out.println(p1.getFirst() + ", " + p1.getLast());
        System.out.println(p2.getFirst() + ", " + p2.getLast());
    }

    static void setSame(Pair<? super Integer> p, Integer n) {
        p.setFirst(n);
        p.setLast(n);
    }

}

class Pair<T> {
    private T first;
    private T last;

    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }

    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
    public void setFirst(T first) {
        this.first = first;
    }
    public void setLast(T last) {
        this.last = last;
    }
}


```

>>>
因此，使用<? super Integer>通配符表示：

允许调用set(? super Integer)方法传入Integer的引用；

不允许调用get()方法获得Integer的引用。

唯一例外是可以获取Object的引用：Object o = p.getFirst()。

换句话说，使用<? super Integer>通配符作为方法参数，表示方法内部代码对于参数只能写，不能读。


```java

// ? extends可以获取安全的引用extends可以安全进行set，不能安全进行get  
// ? super 可以获取安全的T的 super可以安全的进行set 但不不能安全进行get
public class Collections {
    // 把src的每个元素复制到dest中:
    public static <T> void copy(List<? super T> dest, List<? extends T> src) {
        for (int i=0; i<src.size(); i++) {
            T t = src.get(i);
            dest.add(t);
        }
    }
}
```