---
layout: post
section-type: post
title: Basics of Type Parameter & its Bounds in Java Generics
category: java
tags: [ 'java', 'generics']
---
In the last article -  [**Use Cases of Generics**](https://narendranss.github.io/java/2017/06/11/Usecases-of-Generics.html), we saw about Generics &amp; various instance where Generic programming is commonly applied.

In this article we will see an important topic called as  **Type Parameter Bounding** in Java Generics.  Generic Programming and Object Oriented Programming are two different methodology of Programming. Until we see them separately, we are not confused, while we start mixing them up we start getting confused. In the last article,  [**Use Cases of Generics**](https://narendranss.github.io/java/2017/06/11/Usecases-of-Generics.html), we did not bothered much about mixing Object Oriented Programming principles, we were concerned much about  **Data Types** and how to abstract out the data Types to create **Templates** and **Generic Boxes.** In Generic Programming we have no meaning for Objects &amp; Inheritance, every Object is perceived as  **Data**  with  **Data Type. The Structure** we form is perceived as **Data Structure.** Every operation we perform is perceived as Create, Update, Read, Delete, View, Traverse etc., which we normally do on any data structure. Our perception has to change a bit when we work with Generics despite the fact that we cannot completely ignore any OOPS principles &amp; concepts.

**Information**

In this article, the term **&quot;Generic Type&quot;**  usage is avoided and more preference is given to use the term  **&quot;Generic Box&quot;**  and the term  **&quot;Generic Method&quot;**  is avoided and more preference is given to use the term  **&quot;Templates&quot;.** The alternative terms usage helps us to remain conscious about  **Generic Programming** and helps us to visualize them better. At places,  **Generic Box**  and  **Templates**  may not be sufficient enough as they are slightly different from  **Generic Type**  and  **Generic Method**. For example when we use Abstract classes or methods or Interfaces of Java, we will not be able to express them with term Generic Box or Templates, only the concrete implementation can be denoted with the term Generic Box or Templates. At these places, only  **Generic Type**  and  **Generic Method**  remains meaningful.

The purpose usually comes first. I feel it is good to move from  **Generic Box**  and  **Templates** terms usage to  **Generic Type**  and  **Generic Method** terms usage, as we are move from purpose to implementation,

## What is a Type and Type Parameter?

Consider the below example program,  It defines a Generic box. In Java, every class inherits from  **Object.class,** even If a class does not inherits anything explicitly, i.e., If there is no extends keyword, it inherits from Object.class implicitly. So here  **T is Type Parameter**  stands for  **any Object.class Type**. I like to stress the word  **Type.** In Generic, we are more interested about the  **Object Type**  than Object itself.  **Object Type**  is closer or same as  **Data Type.**

<p align="left">
- A class is a <b>type</b>.
<br/>
- An interface is a <b>type</b>.
<br/>
- A primitive is a <b>type</b>.
<br/>
- An array is a <b>type</b>.
</p>

**Java is a type system.** i.e., a system which works on Types or Data Types.

For type like  **Interface**  or  **abstract class,**  Object (i.e., data) cannot be created without assistance of  **class**  type. sometimes we say object is of interface or abstract class type to denote objects from a group of class Type. In order to not complicate, and go step by step, we will take only  **class**  type and then go to interface or abstract type in later examples.

Since Type Parameter T stands for any  **Object Type** , you can put  **any Object** , in below generic box as every class inherits from Object.class &amp; becomes an  **Object Type**.

**Generic Box**

<script src="https://gist.github.com/narendranss/4bf08b1af5bc3869abbdb3718553fde8.js?file=GenericBox.java"></script>

## Why we need to bound Type Parameter?

In this Generics box,  **T** will have access to all methods in **Object.class** like equals(), hashcode() etc., we can actually invoke them. But apart from these methods we will not have access to other methods of the actual Object.

Say, we have a Person Class &amp; its Object instance, In the Generic Box, we can not invoke getName() method which belongs to Person Object despite it is going to get into the Box. We can only get the Person Object out of the generic box and then invoke the Person method getName().

**Person Object in Generic Box**

<script src="https://gist.github.com/narendranss/4bf08b1af5bc3869abbdb3718553fde8.js?file=PersonInGenericBox.java"></script>

## Bounded Type Parameters and Specialized Boxes

We can write  **generic box applicable only for all Objects of Type Person** , because not all Objects of Object.class type has getName() method. We have to create **Specialized Box** to access Person methods, which can be used only by Person Objects &amp; its Children, as not every object has getName() method. It actually requires **Type Bounding**.

While using Collection API, we always take the object out of the Box (ArrayList, LinkedList etc.,) and we mostly work on it only. In Collection API, most of the box type are not bounded, they work mostly on the methods like equal(), hashcode(), wait() etc., present in  **Object.class**

Consider the below code, a Specialized Person Box, which allows only person objects &amp; its children, now the Specialized Box has access to Person Object method getName(). Specialized Box are created with the help of  **Bounded Quantification,** i.e., by Bounding the Type **T**  to special Type.

**Person Box**

<script src="https://gist.github.com/narendranss/4bf08b1af5bc3869abbdb3718553fde8.js?file=PersonBox.java"></script>

## Specialization to Generalization:

We can also create a Named Box, by bounding the Type  **T**  to an Interface Type. So any Object which implements the contract of IName can be dropped into the Named Box and the name can be accessed within the box. In this case, we relaxed the bound from more specific &quot;T extends Person&quot; to little General &quot;T extends IName&quot;. From the examples one thing we could understand is that  **&quot;Type Bounding is all about Generalization &amp; Specialization of Boxes&quot;.** You can also not that now we say object is of Interface IName type, making it applicable for group of class types whichever implements the IName interface.

Consider Collection class  **TreeSet** , you cannot put any Object of Object.class Type, you can put Object of Type Comparable, same applies for the key Object of  **TreeMap**. In the both the cases Type  **T**  is bounded by Comparable Interface (a general interface required for sorting any object). They can be called as Boxes specialized with sorting facility.

**Named Box**

<script src="https://gist.github.com/narendranss/4bf08b1af5bc3869abbdb3718553fde8.js?file=NamedBox.java"></script>

## Type Parameter bounding for Templates

**Type Bounding**  is not just for Boxes, it is also applicable for Generic methods or  **Templates**. Below are examples for Templates with bounds, where  **T**  is bounded by  **&quot;Number&quot; Type.** They are not General Templates applicable for  **Object Type, i.e., all Objects,** they are applicable only for Objects of **Type Numbers,** I can call them as **Specialized Templates.**

**Template with Bound**

<script src="https://gist.github.com/narendranss/4bf08b1af5bc3869abbdb3718553fde8.js?file=Template.java"></script>

## Short Summary on Type Parameter Bounding

Bounding of  **Type parameter T** is done to move from  **Generalization** to **Specialization** and vice versa. Any generalization and specialization achieved with Bounding makes the template or generic box applicable for **a Range of Types**  &amp; not one Type only. By Range of Type, I mean the bound defines it applicability for any Type and all its Sub Type.

In general, you can put or pass objects of  **a type and its sub type**  into box or template but not its super type, it is based on the  **Bound**  we defined. You can access the methods &amp; properties of  **a type and its super type**  with in the box or template but not its sub type methods despite you can pass a sub type object and it is allowed.

## Type Bounding and Type Parameter Bounding

In Order to create Specialized Boxes or Templates so far we used only one Type of  **Bounded Quantification**. The Type which we used is called as  **&quot;Upper Bounding&quot;**  Type, i.e., we made the Specialized Box or Templates applicable for a Type (say Person) and its Sub Types(say employee, manager etc.,)

**Lower Bounding** , and Bounding with **both Lower and Upper Bound**  are other natural options which may come to our mind. If you notice in the above examples, we applied bound in Class Signature or Method Signature i.e., on  **Type Parameters** during the definition of Generic Boxes or Templates. We could also Bound Types during creation of Objects for Generic Types and while invoking Generic Methods, by then we apply type bound on **Type Arguments.** We will see about Type Argument, Substitution failure and Wildcards together in the next coming articles.  **Type Parameters**  can have only  **Upper Bounds**.

We can visualize the boxes we formed in the below picture and it also allows us to visualize the bounding we created.

![](https://s-media-cache-ak0.pinimg.com/originals/8d/59/7d/8d597d6cd5e1ffab11f1348796b69aeb.png)

![](https://s-media-cache-ak0.pinimg.com/originals/a0/6d/41/a06d4157ab48f556ead7227323cac362.png)

In the above diagram, you can visualize both Type Bounding Types and how Type Parameter bounding fits in.

In this article, we saw what is Type and Type Parameter and why we should apply Type Bound and what kind of Type bound is applicable for Type Parameter.