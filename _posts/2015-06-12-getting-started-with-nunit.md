---
layout: post
title:  "Getting Started with NUnit"
date:   2015-06-12 01:00:00 -0600
---

NUnit is not the default testing framework when building .NET applications and
getting it setup can be a little bit tricky. To help alleviate some of the setup
pain this article will walk you though how to get NUnit added to your Solution
and show you how to write your first test.

## Step 1: Create a New Solution

You can use an existing Solution/Project if you have one, but for the sake of
this tutorial we are going to create a new Solution so that we have a blank
slate.

1. Open of Visual Studio
2. Select "New Project..."
3. Name your project NUnitExample
4. Click OK
5. Select the "Web API" template and make sure "MVC" and "Web API" boxes are
checked.
6. Make sure authentication is set to "No Authentication"
7. Click OK

## Step 2: Create a Tests Project

It's a good idea to isolate your tests from your main project so that you can
easily exclude them from running in production. In order to do that we need to
create another project inside of our solution.

1. Right-click on the solution and select Add -> New Project
2. Under `Installed -> Visual C# -> Web -> Visual Studio 2012` Select "ASP.NET
Empty Web Application" 
3. Name the project "NUnitExample.Tests"
4. Click OK

## Step 3: Install the NUnit Package

Now that we have our project setup it is time to install NUnit. There are
probably several different ways to do this but I think the easiest way is to
simply install the NuGet package for NUnit.

1. Open up the Package Manage Console
2. Type: `Install-Package NUnit NUnitExample.Tests` and press enter

The console should have output that looks something like:

```
Installing 'NUnit 2.6.4'.
Successfully installed 'NUnit 2.6.4'.
Adding 'NUnit 2.6.4' to NUnitExample.
Successfully added 'NUnit 2.6.4' to NUnitExample.Tests. 
```

## Step 4: Test the Values Controller

We need a place where we can write our test for the Values Controller. To do
that we can create an empty class file.

1. Right-click on the NUnitExample.Tests project and select Add -> Class...
2. Name the class ValuesControllerTests.cs
3. Click OK

Now we need to setup our test file:

1. Add the following using statement to the top of the file `using
NUnit.Framework;`
2. Add this attribute above the class name: `[TestFixture]`
3. Create a method called `ReturnsAListOfValues`
4. Above that method create an attribute called `[Test]`

Before we start writing our test we will need to add a reference to the
NUnitExample project and add another using statement.

1. Right-click on the NUnitExample.Tests project and select `Add -> Reference...`
2. Select the "Solution" option in the left pane
3. Check the box next to "NUnitExample"
4. Click OK
5. Now add the following using statement to the top of the file: `using
NUnitExample.Controllers;`

Since our test is actually creating an instance of a controller we need to add a
reference to the .NET library responsible for HTTP stuff, like controllers. Open
up the Package Manage Console again and install the following package:

```
Install-Package Microsoft.AspNet.WebApi.Core --Version 5.2.2 NUnitExample.Tests
```

*Note: Version 5.2.2 of WebApi.Core is what I currently have installed in the
NUnitExample project. To verify what version you have installed you can open up
the NUnitExample project, click on References and click for System.Web.Http. In
the Properties window under Version you can see which version you have
installed.*

Now at the top of our file we can add another using statement:

```
using System.Web.Http;
```

Your file should now look like:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using NUnit.Framework;
using NUnitExample.Controllers;
using System.Web.Http;

namespace Tests
{
    [TestFixture]
    class ValuesControllerTests
    {
        [Test]
        public void ReturnsAListOfValues()
        {

        }
    }
}
```

## Step 5: Writing the Test

Now that we finally have everything setup we can begin writing our first test.
Inside of the `ReturnsAListOfValues()` method add the following:

```
string[] expected = { "value1", "value2" };

ValuesController controller = new ValuesController();
var result = controller.Get();

Assert.AreEqual(expected, result);
```

For the first line we created our expected result. In the middle section we
created a new instance of the Values controller and then called the .Get()
method. On the last line we check to see if the two results are equal.

## Step 6: Running the Test

Before we can run the test we actually need to install the NUnit Test Runner.

1. Select `Tools -> Extensions and Updates`
2. On the left pane select "Online"
3. In the search box type 'NUnit'
4. The first result should be NUnit Test Adapter, click install.
5. Click Close

Now to run our tests, from the top menu in Visual Studio, select `TEST -> Run ->
All Tests`. Once the test has finished running you should see a green check mark
next to our test signifying that the test passed.

## Conclusion

Writing the actual test is not too bad, but getting everything set up can take
some effort. The good news is that once you have everything setup you shouldn't
have to do it again.

