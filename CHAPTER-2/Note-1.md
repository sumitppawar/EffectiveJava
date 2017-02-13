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