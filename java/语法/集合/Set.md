### Set

Set用于存储不重复的元素集合，它主要提供以下几个方法：

将元素添加进Set<E>：boolean add(E e)
将元素从Set<E>删除：boolean remove(Object e)
判断是否包含元素：boolean contains(Object e)

```java
public class Main {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        System.out.println(set.add("abc")); // true
        System.out.println(set.add("xyz")); // true
        System.out.println(set.add("xyz")); // false，添加失败，因为元素已存在
        System.out.println(set.contains("xyz")); // true，元素存在
        System.out.println(set.contains("XYZ")); // false，元素不存在
        System.out.println(set.remove("hello")); // false，删除失败，因为元素不存在
        System.out.println(set.size()); // 2，一共两个元素
    }
}

// set的实现是HashSet HashSet仅仅是对HashMap的简单

public class HashSet<E> implements Set<E> {
  // 持有一个HashMap:
  private HashMap<E, Object> map = new HashMap<>();

  // 放入HashMap的value:
  private static final Object PRESENT = new Object();

  public boolean add(E e) {
      return map.put(e, PRESENT) == null;
  }

  public boolean contains(Object o) {
      return map.containsKey(o);
  }

  public boolean remove(Object o) {
      return map.remove(o) == PRESENT;
  }
}

// HashSet 无序的
public class Main {
  public static void main(String[] args) {
      Set<String> set = new HashSet<>();
      set.add("apple");
      set.add("banana");
      set.add("pear");
      set.add("orange");
      for (String s : set) {
          System.out.println(s);
      }
  }
}


// TreeSet有序的
public class Main {
  public static void main(String[] args) {
      Set<String> set = new TreeSet<>();
      set.add("apple");
      set.add("banana");
      set.add("pear");
      set.add("orange");
      for (String s : set) {
          System.out.println(s);
      }
  }
}


```

