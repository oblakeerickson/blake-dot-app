---
layout: post
title:  "C# Conditional Methods"
date:   2015-01-24 01:00:00 -0600
---

In C# you can apply *attributes* to methods. An attribute is simply a square bracket with some text in the middle on the line before a method. Here is a simple example inside of a test class:


```
[TestMethod]
public void SaysHelloWorld()
```

This attribute is used by the testing framework so it knows what methods to run.

Something else you can use with attributes are called *conditional methods* which can be used to have blocks of code that only get run in debug mode. Using a conditional method keeps you from having messy if/else logic always checking if you are in debug mode or not.

Here is an example:

```
[System.Diagnostics.Conditional("DEBUG")]
static void ShowDebugInfo(string message)
{
    Console.WriteLine(message);
}
```

This means that when we call this method and we aren't in debug mode it won't be executed:

```
public static void Main(string[] args)
{
    Console.WriteLine("Hello, world!");
    ShowDebugInfo("my message");
}
```

Inside of Visual Studio to switch between "Debug" and "Release" mode there is a drop down on the toolbar just to the right of the Start Debugging button where you can choose which mode you want to run in.
