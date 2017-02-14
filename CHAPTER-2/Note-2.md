### Use Function Object for Strategy
1. Always define strategy interface, to allow diffrent startegy of same type
2. Strategy Object in same for multiple call, consider to make it singletone.
4. If it object is used only once, then consider using anonymous class of strategy.

#### Comparator from java.util package

```java
public Comparator<T> {
      int compare(T o1, T o2);
}
```


