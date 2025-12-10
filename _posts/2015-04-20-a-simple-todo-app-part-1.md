---
layout: post
title:  "A Simple Todo App - Part 1"
date:   2015-04-20 01:00:00 -0600
--- 

My goal for this two part series is to walk you through building a very basic application that uses Angular on the frontend and ASP.NET Web API on the backend so that you can learn how the two frameworks communicate with one another.

The first thing we are going to do is build out the backend by creating a new C# ASP.NET Web API project, create a TodoItem Model, set up the database with Entity Framework, and create a controller.

Once the backend is all setup we will add Angular to our project and get it talking with our backend.

## Setting up our project

Open Visual Studio 2013 and create a new Visual C# Web application using .NET Framework 4.5. Name the app 'TodoApp' and press OK.

Select the Web API template. The MVC and Web API boxes should be checked. On the right side make sure that the Authentication is set to No Authentication. You can go ahead and uncheck "Host in the cloud" because we won't be discussing deploying our app in this article. Click "OK".

## Creating the TodoItem Model

To create our TodoItem Model right-click on the Models Folder and go to Add->Class. Name the class TodoItem and then press the "Add" button.

Replace all of the using statements with the following two statements:

```
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
```

Now let's add the `Id` and `Name` attributes to our class:

```
public class TodoItem
{
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }
}
```

Now that we have our model created, let's go ahead and build our project so that we can scaffold out our controller. To build the project, select "BUILD" from the top menu bar and select "Build Solution".

## Creating the TodoItems Controller

We are now going to build the controller which creates http endpoints that our Angular application will talk to.

To create the controller right-click on the Controllers folder and select Add and then Controller. A new window will pop up with a list of scaffolds. Select the scaffold labeled: "Web API 2 Controller with actions, using Entity Framework". Then press the "Add" button.

Another little window will pop up labeled "Add Controller". In the Model class dropdown select "TodoItem (TodoApp.Models)". Select the '+' button to create a new Data context class. It should auto-populate with this name: "TodoApp.Models.TodoAppContext", then press the "Add button". Be sure to check the "Use async controller actions" box. Then press the "Add" button.

## Turn on migrations

In order to build our database we are going to use Entity Framework. Entity Framework is used to inspect your models and create database tables based on them. Entity Framework can help out dramatically in keeping your database in sync with any changes you make to your model.

From the Package Manager Console type:

    Enable-Migrations

This command will create a Migrations folder and a new file called Configuration.cs. Inside of this new file add a using statement for our TodoItem model:

```
using TodoApp.Models;
```

Inside of the `Seed` method you can replace the commented out code with:

```
context.TodoItems.AddOrUpdate(x => x.Id,
    new TodoItem() { Id = 1, Name = "Buy Milk" },
    new TodoItem() { Id = 2, Name = "Buy Bacon" },
    new TodoItem() { Id = 3, Name = "Buy Apples" }
    );
```

Now back inside of the Package Manager Console, type:

    Add-Migration Initial
    Update-Database

These commands will populate our database with our TodoItems table and add our initial seed data.

## Wrap Up

This concludes Part 1 where we created the backend for our application. In [Part
2](/2015/05/13/a-simple-todo-app-part-2/) we will create our frontend Angular application.
