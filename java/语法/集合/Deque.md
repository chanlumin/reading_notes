## Deque双端队列

既可以添加到队尾，也可以添加到队首；
既可以从队首获取，又可以从队尾获取。


Queue	Deque
添加元素到队尾	add(E e) / offer(E e)	addLast(E e) / offerLast(E e)
取队首元素并删除	E remove() / E poll()	E removeFirst() / E pollFirst()
取队首元素但不删除	E element() / E peek()	E getFirst() / E peekFirst()
添加元素到队首	无	addFirst(E e) / offerFirst(E e)
取队尾元素并删除	无	E removeLast() / E pollLast()
取队尾元素但不删除	无	E getLast() / E peekLast()
```java 
public class Main {
    public static void main(String[] args) {
        Deque<String> deque = new LinkedList<>();
        deque.offerLast("A"); // A
        deque.offerLast("B"); // B -> A
        deque.offerFirst("C"); // B -> A -> C
        System.out.println(deque.pollFirst()); // C, 剩下B -> A
        System.out.println(deque.pollLast()); // B
        System.out.println(deque.pollFirst()); // A
        System.out.println(deque.pollFirst()); // null
    }
}


// 不推荐的写法:
LinkedList<String> d1 = new LinkedList<>();
d1.offerLast("z");
// 推荐的写法：
Deque<String> d2 = new LinkedList<>();
d2.offerLast("z");

```

### 总结
Deque实现了一个双端队列（Double Ended Queue），它可以：

将元素添加到队尾或队首：addLast()/offerLast()/addFirst()/offerFirst()；
从队首／队尾获取元素并删除：removeFirst()/pollFirst()/removeLast()/pollLast()；
从队首／队尾获取元素但不删除：getFirst()/peekFirst()/getLast()/peekLast()；
总是调用xxxFirst()/xxxLast()以便与Queue的方法区分开；
避免把null添加到队列。