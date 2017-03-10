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

Make Definesive copy whenever needed
---------
1. When not sure about client of code may change state of mutable state, consider to make defensive copy.
2. Try not to consider clone methode while making defensive copy, it has its own side effect.
3. In singleton, make sure you make copy of reference instance mutable variable properly.
4. While checking condition mutable refernce, make sure you first clone then check.
5. By checking first condition then clone may change mutable variable state.
6. Following example shows TIME OF CHECK|TIME OF USER (TOCTOU) attack
```java
//Broken !!!!
public void setDOB(Date dob) {
      Date now = new Date();
      
      if(now.compaireTo(dob) < 0) {
            throws new IllegalArgumentException("DOB must less than than cuurrent date");
      }
      //Make Defensive copy, But after check client make changes in passed dob reference copy 
      this.dob = new Date(dob.getTime());
}


//Correct  first We make defensive copy then check for condition
public void setDOB(Date dob) {
      Date now = new Date();
      
      //Make Defensive copy
      this.dob = new Date(dob.getTime());
    
      if(now.compaireTo(dob) < 0) {
            throws new IllegalArgumentException("DOB must less than than cuurrent date");
      }
}
```

Method Design
---------
1. **Choose method name carefully**, which must follow you package naming convention.
2. Primary goal is to make it readable, understandable, easy to guesse about methods funtionality.
3. **Avoid long list parameters**. Avoid long list method parameter, it is verey hard to remember once list is long.
4. Long list make programmer force to see documention, even it is very hard when metod paramter has same type.
5. Ways to avoid long parametr are 
      1. Builder Pattern (While Conctructing Factory methods)
      2. Holder Static class
      3. Telescopic pattern (Least preferd)
6. **For parameter type favor intefaces over classes**. By doing this you are forced to client to pass specific implemetation.
7. It helps to client to avoid type conversion, if data is in differ format.
8. **Prefer Enum type to boolean Parameter**. It make you code more readable and writable if IDE support autocompletion for enum.
9. Also it helps add more Option for future need.
10. Following example shows Thermometer static factory which takes its scale using boolean and Using enum
```java
// Thermometer with two scale isFarenheit (true), CELSIUS(false)
Thremometer.newInstance(true);

//With Enum
enum ThermometerScale {
 FARENHEIT, CELSIUS
}

//More Readable, and add more option scale if required
Thremometer.newIntance(ThermometerScale.FARENHEIT);
```
