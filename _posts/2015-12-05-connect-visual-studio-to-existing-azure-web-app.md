---
layout: post
title:  "Connect Visual Studio To Existing Azure Web App"
date:   2015-12-05 01:00:00 -0600
---

When creating a new azure web application it is probably faster if you create your new web app from Visual Studio, but I like creating them from the azure portal since I'm usually in there already doing other management stuff. The problem is when I go back into Visual Studio to connect my new web app to azure it isn't quite clear the workflow to use to get your app deployed into azure.

## Step 1: Create a Web App Inside Azure

Sense we are already inside azure let's create a new web app:

1. Click on App Services in the left side bar
2. Click the Add button
3. Give the app a name
4. Click the Create button

After you press the Create button Azure will provision your new web app. When it is done it will take you to the following screen where you can download the "Publish Settings" for your web app


## Step 2: Create a new Visual Studio Project

Now that we have our app created in Azure, let's create our app in Visual Studio.

Open up Visual Studio and select New Project

The "New Project" window should now be opened up.

1. On the right side un-check application insights (unless you want it). This part is actually kind of confusing because even though you can put in your azure credentials this section isn't for selecting your azure web app.
2. Give your project a name
3. Press OK

The "New ASP.NET Project - <project name>" window should now be opened up.

On this screen is where I was getting confused because we are going to be hosting our application in the cloud, but if you check that option, you have to create a new app instead of selecting from a dropdown of existing apps. For this reason we are going to leave this box unchecked and then press OK.

Your project should now be creating

Now open up Solution Explorer and right-click "Publish..."

The "Publish Web" window should now be open. Press the "Import Button"

And browse for the publish settings file we downloaded earlier from our web app inside of azure

Once you have selected the file you can press OK

The "Publish Web" window should change to show the following screen with your app settings. Now press Publish

And now you are done. You have successfully created a web app inside of Azure Portal, downloaded the publish settings file, and connected it to a new Visual Studio project.
