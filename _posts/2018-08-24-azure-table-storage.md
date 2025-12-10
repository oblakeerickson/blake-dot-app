---
layout: post
title: "Azure Table Storage"
date: 2018-08-24 06:00:00
---

One of the things that I like about Azure Table Storage is that it is cheap and
it can be quite fast too if you know the partition key and row key of the thing
you are searching for.

You can actually store several gigs of data for just a few cents every single
month.

One use for table storage could be application log data. Or perhaps there is
some database table in your sql database that is trastically larger than any
other table in your db that you could extract out and store that data in azure
table storage instead?

Here is some key information about Azure Table Storage

- Key-Value based
- Can have 255 properties
- Each entity size can be up to 1mb
- Data is stored by partition key and row key
  - Improve scalability by limiting number of partitions
  - Batch operations can be affected by having a lot of partitions

Supposedly you are only charged the amount of data you are storing, but on the
pricing page it says:

> We charge $0.00036 per 10,000 transactions for tables. Any type of operation
> against the storage is counted as a transaction, including reads, writes, and
> deletes.

So on the Azure 70-532 exam you might need to be careful how you answer a
question about this.

One of the things that I don't always like about using cloud only resources like
Azure Table Storage is that you can't really run them locally on your dev
machine. There is however a [storage emulater][se] you can run locally on Windows and there is
also a non-Microsoft [open source version][os] you can run on Linux, OS X, and Windows.

Another tool to checkout is the [Storage Explorer][ex] which you can use instead
of the Azure portal to view/edit data in your Table Storage account.

[se]: https://docs.microsoft.com/en-us/azure/storage/common/storage-use-emulator
[os]: https://github.com/azure/azurite
[ex]: https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer?tabs=linux
