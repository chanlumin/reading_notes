# Collection，它是除Map外所有其他集合类的根接口

```java
List<String> list = new ArrayList<>();
list.add("apple"); // size=1
list.add("pear"); // size=2
list.add("apple"); // 允许重复添加元素，size=3
System.out.println(list.size());


// java11
List<Integer> list = List.of(1, 2, 5);


// 遍历
List<String> list = new ArrayList<>();
list.add("apple"); // size=1
list.add("pear"); // size=2
list.add("apple"); // 允许重复添加元素，size=3
System.out.println(list.size());
for (int i=0; i<list.size(); i++) {
    String s = list.get(i);
    System.out.println(s);
}
for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
    String s = it.next();
    System.out.println(s);
}
for (String s : list) {
    System.out.println(s);
}

// iterator 是最高效的 而for(String s: list) 也是采用iterator进行遍历的


// 转成数组
Integer[] array = list.toArray(new Integer[3]);
for (Integer n : array) {
    System.out.println(n);
}


String[] array = list.toArray(new String[3]);
for (String n : array) {
    System.out.println(n);
}

// 传入恰好大小的数组
// Integer[] array = list.toArray(new Integer[list.size()]);

// java11
Integer[] array = list.toArray(Integer[]::new);

// array转为list
Integer[] array = { 1, 2, 3 };
List<Integer> list = List.of(array);
// 对于JDK 11之前的版本，可以使用Arrays.asList(T...)方法把数组转换成List。

// 对只读List调用add()、remove()方法会抛出UnsupportedOperationException。
```