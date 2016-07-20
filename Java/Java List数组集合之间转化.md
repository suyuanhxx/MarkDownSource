JAVA的list,set,数组之间的转换，主要是使用Apache Jakarta Commons Collections，具体的方法如下：  
`import org.apache.commons.collections.CollectionUtils;`  
`String[] strArray = {"aaa", "bbb", "ccc"};`    
`List strList = new ArrayList();`    
`Set strSet = new HashSet();`    
`CollectionUtils.addAll(strList, strArray);`    
`CollectionUtils.addAll(strSet, strArray);`   
`CollectionUtils.addAll()`方法的实现很简单，只是循环使用了`Collection`的`add()`方法而已。  
如果只是想将数组转换成List，可以用JDK中的java.util.Arrays类：  
`import java.util.Arrays;`    
`String[] strArray = {"aaa", "bbb", "ccc"};`   
`List strList = Arrays.asList(strArray); `   
**不过Arrays.asList()方法返回的List不能add对象，因为该方法的实现是使用参数引用的数组的大小来new的一个ArrayList。**  
**Collection转数组**  
直接使用Collection的toArray()方法，该方法有两个重载版本：  
`Object[] toArray();`   
`T[] toArray(T[] a);`  
*** 
**Map转Collection**  
直接使用Map的values()方法。 
*** 
**List和Set转换**  
`List list = new ArrayList(new Hashset());// Fixed-size list`
`List list = Arrays.asList(array);// Growable`   
`List list = new LinkedList(Arrays.asList(array));//   Duplicate elements are discarded`   
`Set set = new HashSet(Arrays.asList(array));`//该方法有问题  
***
**List去重**  
`List listWithoutDup = new ArrayList(new HashSet(listWithDup));//不带类型`
`List<string> listWithoutDup = new ArrayList<string>(new HashSet<string>(listWithDup));//带类型`
`List<string> listWithoutDup = new ArrayList<>(new HashSet<>(listWithDup)//JDK7以上写法`
