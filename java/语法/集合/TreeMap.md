#  TreeMap
> 对key进行排序的Map SortedMap遍历的时候回以Key的顺序进行遍历

```java
  public static void main(String[] args) {
      Map<String, Integer> map = new TreeMap<>();
      map.put("orange", 1);
      map.put("apple", 2);
      map.put("pear", 3);
      for (String key : map.keySet()) {
          System.out.println(key);
      }
      // apple, orange, pear
  }
```
# TreeMap 方的Key必须实现Comparable接口，String、和Integer已经实现了Comparable了不进要

```java
public class Main {
    public static void main(String[] args) {
        Map<Person, Integer> map = new TreeMap<>(new Comparator<Person>() {
            public int compare(Person p1, Person p2) {
                return p1.name.compareTo(p2.name);
            }
        });
        map.put(new Person("Tom"), 1);
        map.put(new Person("Bob"), 2);
        map.put(new Person("Lily"), 3);
        for (Person key : map.keySet()) {
            System.out.println(key);
        }
        // {Person: Bob}, {Person: Lily}, {Person: Tom}
        System.out.println(map.get(new Person("Bob"))); // 2
    }
}

class Person {
    public String name;
    Person(String name) {
        this.name = name;
    }
    public String toString() {
        return "{Person: " + name + "}";
    }
}

```
### KeyMap 按照score进行排序
```java
public class Main {
    public static void main(String[] args) {
        Map<Student, Integer> map = new TreeMap<>(new Comparator<Student>() {
          // public int compare(Student p1, Student p2) {
          //     return p1.score > p2.score ? -1 : 1;
          // }
          // keymap在两个值相同的时候要返回0
          public int compare(Student p1, Student p2) {
          if (p1.score == p2.score) {
              return 0;
          }
            return p1.score > p2.score ? -1 : 1;
          }
        });
        map.put(new Student("Tom", 77), 1);
        map.put(new Student("Bob", 66), 2);
        map.put(new Student("Lily", 99), 3);
        for (Student key : map.keySet()) {
            System.out.println(key);
        }
        System.out.println(map.get(new Student("Bob", 66))); // null?
    }
}

class Student {
    public String name;
    public int score;
    Student(String name, int score) {
        this.name = name;
        this.score = score;
    }
    public String toString() {
        return String.format("{%s: score=%d}", name, score);
    }
}
```