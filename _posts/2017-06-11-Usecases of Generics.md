---
layout: post
section-type: post
title: Usecases of Generics
category: java
tags: [ 'java', 'generics']
---
**Understanding general use cases of Generics, Solves half of the Problem.**
**First is first, we should know what is it? why? and where to apply?**

**What is it?**

Consider a simple add method below, you cannot pass long, float, double types as input to this method, isn&#39;t it?

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=Add.java"></script>

If we can abstract out Data Type from the method, we get a new method as below, here  **&lt;T&gt;**  is  **Type parameter** , similar to a parameter we declare for a method, The value we pass  **&lt;Integer&gt;**  or  **&lt;Double&gt;** for the type parameter is the  **Type Argument** , similar to our method argument we pass.

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=GenericAdd.java"></script>

Consider a  **Data Structure**  now, for simplicity let us take Array. Can we create an array of any type? No, we can&#39;t. we can create an array of Integer **, ** Float or of any specific type. Forget about the array implementation of any language and question,  **Can we abstract out the data type from this data structure?**

![](https://s-media-cache-ak0.pinimg.com/originals/40/d2/c4/40d2c4b2aa06a60085312445657e3792.jpg)

**Answer:**  Yes, we can. In Java,  **ArrayList**  is such a class which does it. When you say List&lt;String&gt; = new ArrayList&lt;&gt;(); it creates an array of String. When you pass Integer as type argument instead of a string, it creates an array of Integer and so on.

Despite having said about ArrayList, we cannot get into the implementation of ArrayList, as it is too complicated. So, we shall take a Single box and investigate how to make the box, a Generic box from a Specific Typed box.

![](https://s-media-cache-ak0.pinimg.com/564x/d7/71/ea/d771eaffbed307ac64ce914f127cbb18.jpg)

Consider the below code, you can put a String into SpecilizedStringBox Object and you can get a String out of it.

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=SpecilizedStringBox.java"></script>

Now if we abstract out the Data Type &quot;String&quot; from the SpecilizedStringBox, we get a generic box represented by below code, which can take String, Integer, Boolean and any Data Type of course.

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=GenericBox.java"></script>

**So, Generics is all about abstracting type from a method or a class to create generic methods or class applicable for more type than a specific type.**

# **Why?**

A simple answer will be, to abstract out data type, reuse code and to maintain it better.

# **Where to apply?**

It looks like we can apply Generics by refactoring an existing specific typed method or a box. Until we deal with data structure and primitive data types, It looks easy, but we do create a lot of Data Types with various classes. Mixing Generic Programming Paradigm with OOP paradigm makes it very difficult to make a choice whether or not to apply generics. Understanding where you can apply solves half of the problem.

This article lets you know some of the uses cases of generics where it is generally applied and it also makes sure that you too can apply generics if you encounter such use cases.

Java incorporated Generics in Java 5.0 to achieve,
<p align="left">
1. Type Safety - Ensures that once the type argument is applied, no other data type or type is allowed into the method or box and avoid the requirement of casting.
<br/>
2. Generic Programming / Parametric Polymorphism
</p>

C++ Template Programming helps us to achieve Generic Programming / Parametric Polymorphism, i.e., Same Algorithmic Templates can be morphed according to Data Types (Predefined / User defined) thereby reusing the same code/program.  Nothing different, same is applicable for Java.

Let us see get into the common use cases of Generics.

# **Use Case Type 1:**   **Algorithm and Data Structures are First Class Use Cases for Generics**

Algorithms go hand in hand with Data Structures, i.e., A simple change in Data Structure in an algorithm could change its complexity.

Data in the Data Structure has a Type. Abstracting out this type with Type Parameter is achieved with Generics.

Input parameters of any algorithm have data type. Abstracting out the types from input parameter is achieved with Generics.

So, Generics suit well for any Specific algorithm working with particular Data Structure. In fact, Generics was designed mainly for Collection API of Java.

If you write your own Data Structure, do try to apply Generics. Apart from Java Collection API, you could encounter Generics better use in  [Guava](https://github.com/google/guava),  [Apache Common Collections](https://commons.apache.org/proper/commons-collections/),  [FastUtils](http://fastutil.di.unimi.it/),  [JCtools](https://github.com/JCTools/JCTools), and  [Eclipse Collections](https://www.eclipse.org/collections/).

# **Use Case Type 2: Value Typed Boxes or Single Element Container**

Data Structures with Generics Type are Generic Boxes. Classes such as ArrayList, LinkedList etc., represent Data Structures and acts as Generics Boxes of their kind.

Sometimes Generic boxes do appear as a single element instead of a collection. They just act as Holders or Wrappers of Data of a particular Data Type. egs., Entry&lt;K, V&gt; in a Map, Node&lt;K,V&gt;,  Pair&lt;K, V&gt;, Algebraic Data Types like Optional&lt;T&gt;, Choice&lt;U, V&gt;  etc., etc.,

[**ThreadLocal**](https://docs.oracle.com/javase/8/docs/api/java/lang/ThreadLocal.html),  [**AtomicReference**](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/AtomicReference.html) are very good examples of Single Element Containers which apply algorithms required for concurrent access.

Such use cases sometimes justify the use case and sometimes not. A Box can hold any type of article, earlier we can put anything into a box, now we classify, this box is for toys, the next box is for pens etc.,

![](https://s-media-cache-ak0.pinimg.com/originals/00/fb/f7/00fbf7334335a4aebd5c0ea84e35ee4f.png)


A Cup as a Holder can hold either Tea or Coffee or any beverage. Cup is a good example of real-time object Type (Tea, Coffee..) holder. A Bus can carry both Men or Women, If we make it type safe to allow only Women, we can call it as Ladies/Women Bus. Needless to say, it may be or may not be appropriate. The catch is business use cases especially wrappers or Holder also provide opportunities to apply Generics. Question, whether the business Wrapper or Holder usage is inclined towards data structure kind of use, if so, generics usage will do better.

![](https://s-media-cache-ak0.pinimg.com/originals/eb/d6/7d/ebd67df7da0c98dd951e3b05628f5715.jpg)

# **Use Case Type 3: Generic Util Methods with Abstract Classes**

Generic Algorithms need not be always tied to particular Data Structures or Algorithm, sometimes it can be applied to most abstract Group of Data Structures based on the Contract the Concrete Implementations Satisfy.

In Java, we have &quot; **Collections**&quot; util Class.

Check the below method from the class to get an idea of what kind of methods can be implemented.

**Collection Factories methods (empty, singleton):**
<p align="left">
emptyList, emptyMap, emptySet, etc.,
<br/>
singleton, singletonList, singletonMap etc.,
</p>

**Wrapper Methods (synchronized, UnModifiable, Checked Collection):**
<p align="left">
synchronizedCollection, synchronizedSet, synchronizedMap, etc.,
<br/>
unmodifiableCollection, unmodifiableSet, unmodifiableList, etc.,
<br/>
checkedCollection, checkedList, checkedSet, etc.,
</p>

**Few more generic methods fall into four major categories:**
<p align="left">
1. Changing element order in a list -  reverse, rotate, shuffle, sort, swap
<br/>
2. Changing the contents of a list - copy, fill, replaceAll
<br/>
3. Finding extreme values in a collection - max, min
<br/>
4. Finding specific values in a list - binarySearch, indexOfSubList, lastIndexOfSubList
</p>

They represent reusable functionality, in that they are applied to Lists (or in some cases to Collections) of any type. We can find a lot of Generics methods applicable to most of the Collection Types in General.

# **Use Case Type 4: Generic Methods in Parallel Hierarchy of Classes**

[**JpaRepository**](http://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html),  [**CrudRepository**](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html) in  **Spring Framework**  have been build with Generics Usage. The Create, update, find, findAll, delete etc., are generic methods applicable for all Entities.

For Every Entity, a parallel DAO class required to be created, hence a  [**Parallel Hierarchy of Classes**](http://wiki.c2.com/?ParallelInheritanceHierarchies) appears in these cases. DAO pattern is not the only case where such  **Hierarchy of Parallel classes**  appears.

It usually occurs if we apply Strategy Pattern to solve our Business Problem by decoupling the method from an object, to supply many possible instances of the method.

Whenever we add a new class, we do add a parallel Test case. if we require factories, we do add parallel factory class. Parallel hierarchy of classes do occur in business use cases, consider a new vehicle say &quot;Bus&quot; is added to below vehicle hierarchy, in that case, we may be in the requirement to add &quot;Bus Driver&quot; class.


<img src="https://s-media-cache-ak0.pinimg.com/originals/49/6e/7a/496e7af9f3e2e90e9c8896961da04226.png" alt="" style="width:650px;"/>

<img src="https://s-media-cache-ak0.pinimg.com/originals/9d/e3/03/9de303f3e0a11b02932bd9bc645b79c3.png" alt="" style="width:650px;"/>

Below is an example for Parallel Hierarchy of Classes and Generics.

<img src="https://s-media-cache-ak0.pinimg.com/originals/bc/ef/e4/bcefe4c6102352f1a4e2837050b3bdea.png" alt="" style="width:650px;"/>
 
<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=Habitat.java"></script>

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=Aquarium.java"></script>

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=Animal.java"></script>

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=Fish.java"></script>

<script src="https://gist.github.com/narendranss/a719ad5ec39de590b3970e8d3279c1b0.js?file=TestHabitat.java"></script>

# **Use Case Type 5: To Create Type Safe Heterogeneous Containers**

Collection&lt;String&gt; is an example of  **Homogeneous Container** , i.e, you cannot put anything other than String into the box. Collection&lt;Object&gt; is an example of  **Heterogeneous Container**  i.e., you can put any object into this box.  Collection&lt;Object&gt; is not Type safe. You need to check for type and cast it,  **similar to Raw Type &quot;Collection&quot;**  (a raw type is a Generic Type without Generic Type Argument applied, it takes Object as default Type Argument).  **Java does not provide a first class support for Type Safe Heterogeneous Container**.

In Collection&lt;String&gt;,  Type Argument &quot;String&quot; is applied for Type Parameter &quot;T&quot; to make it type safe. Consider Map&lt;String, String&gt;, it takes 2 Type Arguments here. The normal use of generics, exemplified by the collections APIs, restricts you to a ** fixed number of type parameters**  per container. You can get around this restriction by placing the  **type parameter on the key of a Map, rather than the container**.  You can use  **Class objects as keys**  for building  **Typesafe heterogeneous containers or maps**.

Containers such as bean creation container, exception handler containers, service lookup containers are examples of  **Heterogeneous Containers**  where generics can be used to make it type safe with dynamic casting with Class Objects as key.

I am not giving any code example for Heterogeneous Containers, as a dedicated article will be published on the same. You can also look for Heterogeneous Containers in Google in the mean time.

Hope next time when you think about generics, you will get  **data structure**** s, boxes,  Collections.class methods, Parallel Hierarchy of Classes and heterogeneous Containers **comes up in your mind as well. If you think you know any other use case where Generics can be applied in general, I will be glad to hear from you :)