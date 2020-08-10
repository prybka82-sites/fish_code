---
layout: post
title:  "Attributes in C#"
categories: posts
tags: csharp, dotnet
---

## Introduction

Attributes are C# mechanism for adding metadata to a piece of code in a declarative way, e.g. 

{% highlight csharp %}
[SomeAttribute]
public class MyClass
{
}
{% endhighlight %}

## Creating and using attributes

Attributes are classes inheriting from the ``Attribute`` base class:

{% highlight csharp %}
public class MyAttribute : Attribute
{
}
{% endhighlight %}

Conventionally, attribute name contains the ``Attribute`` suffix, but it may be left out when using the attribute: 

{% highlight csharp %}
[My]
public void Foo() {}

//or

[MyAttribute]
public void Foo() {}
{% endhighlight %}

Using an attribute is in fact invoking its constructor: 

{% highlight csharp %}
public class MyAttrybute : Attribute
{
    public MyAttribute(string someText, int someNumber, bool someBool) { }
}

//...

[My("invoking MyAttribute", 123, true)]
public class MyClass
{ }
[MyAttribute]
public void Foo() {}
{% endhighlight %}

## Restricting attribute usage

Attributes may be added to many types of targets: 

{% highlight csharp %}
using System;

[assembly: MyNamespace.My]              //assembly attribute
[module: MyNamespace.My]                //module attribute
namespace MyNamespace
{
    [My]                                //interface attribute
    public interface IMyInterface
    { }

    [My]                                //delegate attribute
    public delegate void MyDelegate();

    [My]                                //enum attribute
    public enum MyEnum { }

    [My, Other]                         //class attribute, many attributes
    public class MyClass
    {
        [My]                            //field attribute
        private int field;

        [My]                            //property attribute
        public int MyProperty { get; set; }

        [My]                            //constructor attribute
        public MyClass() { }

        [My]                            //event attribute
        public event MyDelegate MyEvent;

        [My] //or: [method: My]         //method attribute
        [return: My]                    //return value attribute
        public int Foo([My] int x)      //parameter attribute
        {
            return 0;
        }
    }
}
{% endhighlight %}

## Attribute functions

If not specifically designed, attributes may have no function just like comments. 

Attributes may be looped through using ``GetCustomAttributes`` method of ``TypeInfo`` class from ``System.Reflection`` namespace: 

{% highlight csharp %}
using System.Reflection;

//...

public void Foo()
{
    TypeInfo typeInfo = typeof(MyClass).GetTypeInfo();

    var attributes = typeInfo.GetCustomAttributes();

    foreach (var attr in attributes)
    {
        System.Console.WriteLine(attr.GetType().Name);
    }
}
{% endhighlight %}

## Most important .NET Core attributes

- ``[Obsolete]`` -- indicates, that a particular piece of code is obsolete. It is advisable to provide information, e.g. 

{% highlight csharp %}
[Obsolete("This class is obsolete. Use MyNewClass")]
public class MyClass
{ }
{% endhighlight%}

- ``[CallerMemberName]`` -- a parameter attribute defined in ``System.Runtime.CompilerServices`` namespace. It injects the name of the method that calls the method containing the attribute, e.g. 

{% highlight csharp %}
public class MyClass : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    public void RaisePropertyChanged([CallerMemberName] string propertyName = null)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }

    private string _name;
    public string Name
    {
        set
        {
            if (value != _name)
            {
                _name = value;
                RaisePropertyChanged(); //parameter is not needed 
                                        //the attribute will pass the caller name
            }
        }
    }
}
{% endhighlight%}

## Source

- [Use Attributes in C#](https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/attributes)