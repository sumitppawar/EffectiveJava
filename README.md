EffectiveJava Notes


Common Names For Static Factory
---------
```java

valueOf()  
//Return an instance of which same value as passed value. This method noramly used for type conversion.
//Example
//Returns Integer equevalent to passed integer
Interger.valueOf(String intValue) 

//Method 
of()
//A consice alternative of valueOf() method, popularly used for EnumSet.
//Example
EnumSet<Color> yellow = EnumSet.of(Color.RED, Color.GREEN);

//Method
getIntance()
//Get intance build by using passed paramter, but can not said have same value as passed. 
//It may be do some conversion before build intance.
//If it used for Singleton then, it will not take any parameter.

//Example
Connection.getInstance()

//Method
newIntance()
//Return always new instance based on passed paramter.

//Example
Connection.newInstance(String url)

//Method
getType()

//This metohd is like getIntance(), except it will return Object of type.
//Example
List<String> list = CSVFile.getList()

//Method
newType()
//This method is like newInstance() return type object as metioned in method name.
//Example
Context context = HttpServeletRequest.getContext()
```

Use Function Object for Strategy
---------
1. Always define strategy interface, to allow diffrent startegy of same type
2. Strategy Object in same for multiple call, consider to make it singletone.
4. If it object is used only once, then consider using anonymous class of strategy.
5. **Comparator from java.util package**

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

Use overloading judiciously 
---------
1. Overloading is determined at **compile time**.
2. So whatever type know at compile time is considered for method invocation .
3. When writing API make sure it is not confusing for radical diffrence type paramter, we can't guess which should get call.
4. Better choice for overloading is to use properNamed method instead of overload.
5. Thumb rule is **Never overload a method with same numbers of parameter(Radically same)**.
6. Following Example shows confusing code
      ```java
      public void print(Set<String> c) {
          System.out.println("Set");
      }

      public void print(List<String> c) {
          System.out.println("List");
      }

      public void print(Collection c) {
            System.out.println("Unknown Collection");
      }

      public static void main(String[] args) {
            Collection[] collections = {new HashSet(), new ArrayList()}
            for(Collection c : collections) {
                  print(c); // Always print "Unknown Collection",  compile time know type is Collection
            }
      }
      ```
7. Alaways take care while calling overload method which may involved autoboxing.
8. Following example shows autoboxing issue
      ```java
            List<Integer> lsInterger = new ArrayList();
            for(int i =-2; i<3;i++) {
                  lsInterger.add(i);
            }
            for(int i=0; i<2;i++) {
            
                  lsInteger.remove(i);//It removes  o 1 2 instead of -2 -1 0 
                  //i is boxed to Interger an overloaded method remove(E) is called instead remove(index)
            }
      ```
Use varargs judiciously 
---------
1. Java 1.4 added varargs.
2. Use varags when input length is unknown to method.
3. Using varargs we cant force user to pass at least require data, don't use varags in this condition.
4. Consider following examples , shows good and bad code.
      ```java
            public Map<String,String> getPersonAttribute(String... args) {
                  String id = args[0]; //Must required
                  ......
            }
            //Instead use following way
            public Map<String,String> getPersonAttribute(String personId, String... args) {
                  ......
            }
      ```
5. There is cost for creation of array for each varargs even you are passing one argument.
6. If it sure and require minimum paramter, don't pass it using varagrs.
7. Example shows a correct way to handle above sentence
      ```java
      //Not Best way
      public void method(String... args) {
            String req_1 = args[0];
            String req_2 = args[0];
            //Don with remainign if provided
      }
      //Best way, if not given any varargs argument , we avoide cost of creation of array
      public void method(String req_1, String req_2, String... args) {
      }
      ```
      
Return Empty Array or Collection instead of null
---------
1. Always return Empty array or collection instead of null,it will avoid client code to take care of null return.
2. If developer forgot to handle such case, it may cause NullPointerException Or developer has to check document about method returns.
3. For collection use ```java Collections.emptyList()``` ,like collection methods.

Write doc comments for all exposed API elements
---------
1. If API is usable, always document it using java doc commects (```java /** Doc comment*/).
2. Write doc comment for every exported **class, method, constructor, field**.
3. If class is serializable, we should also document its serializable form.
4. The doc comment for a method should describe the contract between method and its client.
5. Doc should says what method does rather than how it does.
6. Doc of method should specify percondition , postcondition and side effect.
7. Finally add thread safety of class and method.
8. How to write document for method
      1. To define methods contract fully, method should use 
      2. @param  for parameter, should not terminate with period
      3. @return for return value, should not terminate with period
      4. @throws if methods thorws any Exception, should not terminate with period
      5. {@code} to write code, instead use HTML code tag.
      6. {@inheritDoc} to inherit doc from class or interface.
      7. {@literal} to avoid processing of HTML element (<, > brackets)
      8. First line should explain what method does and end with period.
      9. Following first line with end period ,write detail paragraph using **p** tag without end of it.
      10. @return and @param tag shoud have noun after them
            ```java
            ```
      
9. No two class constructor or interface method with same number of parameter have same first description line.
10. When documenting Enum make sure, to document each constant.
      ```java
      ```
11. When using generic for method or class , make sure you documnent all type.
      ```java
      ```
