# EffectiveJava Notes

### Common Names For Static Factory

```
Method 
valueOf()  

Return an instance of which same value as passed value. This method noramly used for type conversion.

//Example
//Returns Integer equevalent to passed integer
Interger.valueOf(String intValue) 
```

```
Method 
of()

A consice alternative of valueOf() method, popularly used for EnumSet.

//Example
EnumSet<Color> yellow = EnumSet.of(Color.RED, Color.GREEN);

```

```
Method
getIntance()
Get intance build by using passed paramter, but can not said have same value as passed. 
It may be do some conversion before build intance.
If it used for Singleton then, it will not take any parameter.

//Example
Connection.getInstance()

```
```
Method
newIntance()
Return always new instance based on passed paramter.

//Example
Connection.newInstance(String url)

```

```
Method
getType()

This metohd is like getIntance(), except it will return Object of type.

//Example

List<String> list = CSVFile.getList()

```
```
Method
newType()
This method is like newInstance() return type object as metioned in method name.

//Example
Context context = HttpServeletRequest.getContext()
```
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
Always check method parameter
---------
1. Always check method paramter, document what happen if when method get invalid parametr.
2. If not checked replace with it good document about it.
3. If not document or not checked  it is very hard do determine to detect cause.
4. Sometime need to debug code to find cause.
