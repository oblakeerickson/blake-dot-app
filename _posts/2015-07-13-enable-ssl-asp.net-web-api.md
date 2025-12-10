---
layout: post
title:  "Enable SSL In ASP.NET Web API"
date:   2015-07-13 01:00:00 -0600
---

The other day I spent way more time trying to figure out why I couldn't run
[Todo App][1] locally than I really wanted to have. The main thing that was
driving me nuts was that it worked fine the day before. The good news is that I
figured out my issue which let me to write this post on how to enable SSL in
ASP.NET Web API applications.

Enabling SSL for any web application that requires a login is important to keep
data encrypted. For development we are just going to to use a self signed cert,
but if you are using Azure to deploy your web app it will automatically use
Azure's cert if you are on a sub-domain.

## Turn on SSL

To Enable SSL left click on your Project in Visual Studio and the properties
window should open up at the bottom right. Inside of the SSL Enabled row toggle
the value to `True`. Right below there should be another row called SSL URL
which should have a value something like: `https://localhost:44300/`.

## Force HTTPS for the entire app

Rather than adding an attribute to every single controller in our web app we can
apply a global filture that will require https to be used.

Inside of the `App_Start` folder open up the `FilterConfig.cs` file and add the
following line to the existing method:

```
filters.Add(new RequireHttpsAttribute());
```

## Set the project Url

Just to double check since this was the problem I was having you need to make
sure the project URL is using the new https url and not the old http url. To
change the project URL right-click on your project and select Properties from
the bottom of the dropdown. This should open up a section with a bunch of tabs
down the left column. Select the 'Web' tab and under the 'Servers' section make
sure the 'Project Url' is set to:

```
htts://localhost:44300/
``` 

Now when you press the green play button to debug (F5) your selected browser
should open up with the new url.

[1]: https://tdapp.azurewebsites.net/#/
