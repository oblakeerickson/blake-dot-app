---
layout: post
title:  "How To Create A Reserved IP For An Azure VM"
date:   2015-12-19 01:00:00 -0600
---

If you would like to create a reserved IP address for an azure VM using the Portal you will need to create a new VM, from what I can tell you can't use the Portal to assign a reserved IP to an existing VM. You also cannot use the old management portal to create a reserved IP.

Here is the IP Address section for an existing VM and as you can tell there isn't a reserved IP option:

![](https://blakeerickson.blob.core.windows.net/blog/20151219-existing-vm.jpg)

Here are the steps to create a reserved IP for a new VM using the Azure Portal:

**(1)** The first thing we need to do is to create a new VM. Inside of the Azure Portal select the "Virtual machines (classic)" section and then click the "Add" button:

![](https://blakeerickson.blob.core.windows.net/blog/20151219_01.jpg)

**(2)** From the "Compute" blade, select "Windows Server":

![](https://blakeerickson.blob.core.windows.net/blog/20151219-02.jpg)

**(3)** From the "Windows Server" blade click on "Windows Server 2012 R2 Datacenter":

![](https://blakeerickson.blob.core.windows.net/blog/20151219-03.jpg)

**(4)** From the "Windows Server 2012 R2 Datacenter" blade make sure the "Classic" deployment model is selected and press create:

![](https://blakeerickson.blob.core.windows.net/blog/20151219-04.jpg)

**(5)** From the "Create VM" blade. Type in the "Host Name", "User name", and "Password". Then select the "Pricing Tier" and the "Resource Group". Once all of those things have been configured you can then click on "Option Configuration - Network, storage, diagnostics":

![](https://blakeerickson.blob.core.windows.net/blog/20151219-05.jpg)

**(6)** From the "Optional config" blade select the "Network" section:

![](https://blakeerickson.blob.core.windows.net/blog/20151219-06.jpg)

**(7)** From the "Network" blade select "IP Addresses - Virtual, instance, private":

![](https://blakeerickson.blob.core.windows.net/blog/20151219-07.jpg)

**(8)** In this step we are going to configure our Reserved IP address. Which means we are going to give it a name, but we can't actually choose what our IP address will be.

1. From the "IP addresses" blade change the "Virtual IP address" toggle from Dynamic to Reserved.
2. Select "Reserved IP Address - *Not configured*"
3. From the "Reserved IP address" blade select "Create a reserved IP address"
4. From the "Create a reserved IP address" blade give your reserved IP a name.
5. Still inside the "Create a reserved IP address" blade click OK
6. The "Reserved IP Address" blade should have closed automatically for you, so from the "IP address" blade select OK

![](https://blakeerickson.blob.core.windows.net/blog/20151219-08.jpg)

**(9)** Click OK and click Create:

1. From the "Network" blade click "OK"
2. From the "Optional config" blade click "OK"
3. From the "Create VM" blade click "Create"

![](https://blakeerickson.blob.core.windows.net/blog/20151219-09.jpg)

**(10)** Once your VM has been created lets see what are Reserved IP address is. Select the VM that you created:

![](https://blakeerickson.blob.core.windows.net/blog/20151219-10.jpg)

**(11)** From the "Settings" blade click on the "IP addresses" section

![](https://blakeerickson.blob.core.windows.net/blog/20151219-11.jpg)

**(12)** From the "IP addresses" blade you can now see your Reserved IP Address

![](https://blakeerickson.blob.core.windows.net/blog/20151219-12.jpg)

Here is a gif that I made showing all the steps above:

![](https://blakeerickson.blob.core.windows.net/blog/20151219-13.gif)
