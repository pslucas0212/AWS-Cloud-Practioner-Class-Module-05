# Storage and Databases

[AWS Cloud Practitioner Home](https://github.com/pslucas0212/AWS-Cloud-Practioner)

### Introduction

### Transcript

Well, we have quite a coffee operation going now. We've got customers, lots of happy customers. In fact, we have an elastic, scalable, disaster resistant, cost optimized architecture that now has a global, highly secured network that can be deployed entirely programmatically.

You know, now we need some way to show our appreciation to all our loyal customers. How about a frequent drinker loyalty program? Or we could just hand out punch cards, but let's be honest, we can't track those well and use them to get to know our customers better. 


We need digital cards, which means we need to be able to keep track of our customers, what they order, how much they purchased. This will help them, the customers, get the best rewards they've earned and help us to know our customer base better. 


This means we need databases. Databases, and storage. And not just any database. We need to make sure we choose the right database for the task and the right storage for data types.

Now you may have many different data usage needs and data types. Let's learn about the different services AWS has to help you build the perfect data solution.

### Instance stores and Amazon Elastic Block Storage (EBS)

Applications often need access Block Level Storage.  Store data in a set of blocks.  Good for databases, etc.

Block storage could simply be your hard drive.

EC2 provides you with Instance Store Volumes.  Write to it just like a harddrive. But if you stop or delete you EC2 instance, the storage is lost.  THis because if you stop your instance, it could start on another host machine.  Do not write important data to EC2 instance storage volume

Amazon Elastic Block Volumens (EBS) are separate virtual drives that's not part of your EC2 instance volume.

You define size and type of EBS volume you need and attach it to your EC2 instance.

EBS allows you to take incremental backups of you EBS volume  called EBS snapshots for backup purposes


#### Transcript
When you're using Amazon EC2 to run your business applications, those applications need access to CPU, memory, network, and storage. EC2 instances give you access to all those different components, and right now, let's focus on the storage access. As applications run, they will oftentimes need access to block-level storage. 


You can think of block-level storage as a place to store files. A file being a series of bytes that are stored in blocks on disc. When a file is updated, the whole series of blocks aren't all overwritten. Instead, it updates just the pieces that change. This makes it an efficient storage type when working with applications like databases, enterprise software, or file systems. 


When you use your laptop or personal computer, you are accessing block-level storage. All block-level storage is in this case is your hard drive. EC2 instances have hard drives as well. And there are a few different types. 


When you launch an EC2 instance, depending on the type of the EC2 instance you launched, it might provide you with local storage called instance store volumes. These volumes are physically attached to the host, your EC2 instances running on top of. And you can write to it just like a normal hard drive. The catch here is that since this volume is attached to the underlying physical host, if you stop or terminate your EC2 instance, all data written to the instance store volume will be deleted. The reason for this, is that if you start your instance from a stop state, it's likely that EC2 instance will start up on another host. A host where that volume does not exist. Remember EC2 instances are virtual machines, and therefore the underlying host can change between stopping and starting an instance. 


Because of this ephemeral or temporary nature of instance store volumes, they are useful in situations where you can lose the data being written to the drive. Such as temporary files, scratch data, and data that can be easily recreated without consequence.

 

All right, I'm telling you not to write important data to the drives that come with EC2 instances. I'm sure that sounds a bit scary because obviously you'll need a place to write data that persists outside of the life cycle of an EC2 instance. You don't want your entire database getting deleted every time you stop an EC2 instance. Don't worry, this is where a service called Amazon Elastic Block Store, or EBS, comes into play. 


With EBS, you can create virtual hard drives, that we call EBS volumes, that you can attach to your EC2 instances. These are separate drives from the local instance store volumes, and they aren't tied directly to the host that your EC2 is running on. This means, that the data that you write to an EBS volume can persists between stops and starts of an EC2 instance. 


EBS volumes come in all different sizes and types. How this works, is you define the size, type and configurations of the volume you need. Provision the volume, and then attach it to your EC2 instance. From there, you can configure your application to write to the volume and you're good to go. If you stop and then start the EC2 instance, the data in the volume remains. 


Since the use case for EBS volumes is to have a hard drive that is persistent, that your applications can write to, it's probably important that you back that data up. EBS allows you to take incremental backups of your data called snapshots. It's very important that you take regular snapshots of your EBS volumes This way, if a drive ever becomes corrupted, you haven't lost your data. And you can restore that data from a snapshot.

### Amazon Simple Storage Services (S3)

S3 is a datastore that allows you to store and retreive data as long as need.  The data is stores as objects in buckets instead of folders.  Max size is 5 TB and can version objects.   Create mutlipe buckets and control access to data. 

Object storage consists of the data objects, metadata and a key.  Object storage changes the entire object when it changes where block storage only changes (overwrites) blocks that change.

Tiers of S3
- Amazon S3 standard high reliability of not losing data.  Data is stored in 3 AZs.  Useful for static web site storage by enabling bucket to host web content
- S3 Standard Infrequent Access (S3  Standard -IA) is long term storage for infrequently accessed data like backup.  Data is stored in 3 AZs
- S3 Intelligent-tiering Monitors objects' access patterns and automatically moves the object to the best S3 tier
- S3 One Zone-infrequent Access (S3 One Zone-IA)
- Amazon S3 Glacier is for data long term renteion..  Create locked volume policy such as write once read many (WORM)
- S3 Glacier Deep Archive

You can create S3 lifecycle polices that automaticall move data for you between S3 tiers.

Also S3 AI One zone and S3 Glaicer Deep archive.

#### Transcript
Welcome to this video on Amazon Simple Storage Service, or S3. From the name, you've probably guessed that it is a storage service and it's, well, simple. Most businesses have data that needs to be stored somewhere. For the coffee shop, this could be receipts, images, Excel spreadsheets, employee training videos, and even text files, among others. Storing these files is where S3 comes in handy because it is a data store that allows you to store and retrieve an unlimited amount of data at any scale. 


Data is stored as objects, but instead of storing them in a file directory, you store them in what we call buckets. Think of a file sitting on your hard drive, that is an object and think of a file directory, that is the bucket. The maximum object size that you can upload is five terabytes. You can also version objects to protect them from accidental deletion of an object. What this means is that you always retain the previous versions of an object, as like a paper trail. You can even create multiple buckets and store them across different classes or tiers of data. You can then create permissions to limit who can see or even access objects. 


And you can even stage data between different tiers. These tiers offer mechanisms for different storage use cases such as data that needs to be accessed frequently, versus audit data that needs to be retained for several years. Let's go through the notable ones, shall we? 


The first here is called S3 Standard and comes with 11 nines of durability. That means an object stored in S3 Standard has a 99.999999999 percentage – that's a lot of nines –  probability that it will remain intact after a period of one year. That's pretty high. Furthermore, data is stored in such a way that AWS can sustain the concurrent loss of data in two separate storage facilities. This is because data is stored in at least three facilities. So multiple copies reside across locations. Another useful way to use S3 is static website hosting, where a static website is a collection of HTML files and each file is akin to a physical page of the actual site. You can do this by simply uploading all your HTML, static web assets, and so forth into a bucket and then checking a box to host it as a static website. You can then enter the bucket's URL and ba-bam! Instant website. And we say static, but that doesn't mean you can't have animations and moving parts to your website. Pretty awesome way to start up that coffee blog. 


The next storage class is called S3 Infrequent Access or S3-IA. Which is used for data that is accessed less frequently but requires rapid access when needed. This means it's a perfect place to store backups, disaster recovery files, or any object that requires a long-term storage. 


Another storage class or tier lends itself to that example we had earlier about audit data. Say, we need to retain data for several years for auditing purposes. And we don't need it to be retrieved very rapidly. Well, then you can use Amazon S3 Glacier to archive that data. To use Glacier, you can simply move data to it, or you can create vaults and then populate them with archives. And if you have compliance requirements around retaining data for, say, a certain period of time, you can employ an S3 Glacier vault lock policy and lock your vault. You can specify controls such as write once/ read many, or WORM, in a vault lock policy and lock the policy from future edits. Once locked, the policy can no longer be changed. You also have three options for retrieval, which range from minutes to hours, and you have the option of uploading directly to Glacier or using S3 Lifecycle policies. 


Fact, I don't think we mentioned lifecycle policies up till this point. But they are policies you can create that can move data automatically between tiers. For example, say we need to keep an object in S3 Standard for 90 days, and then we want to move it to S3-IA for the next 30 days. Then after 120 days total, we want it to be moved to S3 Glacier. With Lifecycle policies, you create that configuration without changing your application code and it will perform those moves for you automatically. It's another example of a managed AWS service, helping take that burden off you, so you can focus on more of your business needs. 


Just to note that there are other storage classes. Like S3 Infrequent Access One Zone and S3 Glacier Deep Archive that you can use. Happy storing.

### Comparing Amazon EBS and Amazon S3

EBS 
- 16 TiB
- Survive EC2 Instance termination
- SSDsby default
- HDD Option

S3
- unlimited storage
- Maximum Option size5TB size
- WORM
- 99.9999999%


Use Case 1 - Photo analysis website.  Customers upload pictures to determine animal
- S3 is the best solution - Web enabled, Regonally distributred (no need to worry about backup strategy).
- Less exapnesive then EBS, no EC2 instances needed

Use Case 2 - 80 GB video that needs to be edited.
- S3 great for documents and video files that are consumed as a complete ojbect.  When you change a doc, the whole doc is updated
- EBS only updates blocks where bits are changed
- EBS is best choice

If you use complete objects with few changes, S3 is best.  If you do complex data updates then EBS is the best choice


#### Transcript
AWS Cloud Practitioners, welcome to the clash of the storage class! In the block storage corner, weighing in at sizes up to 16 tebibytes each, with a unique ability to survive the termination of their Amazon EC2 instances, they are solid state, they are spinning platters, they are Amazon Elastic Block Storage! 


In the regional object storage corner, weighing in at unlimited storage, with individual objects at 5,000 gigabytes in size, they specialize in write once/read many, they are 99 .999 999 999% durable, they are Amazon Simple Storage Service! 


Head-to-head, each storage class boasts the best dynamically distributed design for different storage demands. Which storage class will ultimately be victorious in this thunderdome slugfest? To understand who wins, you need to clarify a use case. 


Round one. Let's say you're running a photo analysis website where users upload a photo of themselves, and your application finds the animals that look just like them. You have potentially millions of animal pictures that all need to be indexed and possibly viewed by thousands of people at once. This is the perfect use case for S3. S3 is already web enabled. Every object already has a URL that you can control access rights to who can see or manage the image. It's regionally distributed, which means that it has 11 nines of durability, so no need to worry about backup strategies. S3 is your backup strategy. Plus the cost savings is substantial overrunning the same storage load on EBS. With the additional advantage of being serverless, no Amazon EC2 instances are needed. Sounds like S3 is the judge's winner here for this round. 


But wait, round two, you have an 80-gigabyte video file that you're making edit corrections on. To know the best storage class here, we need to understand the difference between object storage and block storage. Object storage treats any file as a complete, discreet object. Now this is great for documents, and images, and video files that get uploaded and consumed as entire objects, but every time there's a change to the object, you must re-upload the entire file. There are no delta updates. Block storage breaks those files down to small component parts or blocks. This means, for that 80-gigabyte file, when you make an edit to one scene in the film and save that change, the engine only updates the blocks where those bits live. If you're making a bunch of micro edits, using EBS, elastic block storage, is the perfect use case. If you were using S3, every time you saved the changes, the system would have to upload all 80 gigabytes, the whole thing, every time. EBS clearly wins round two. 


This means, if you are using complete objects or only occasional changes, S3 is victorious. If you are doing complex read, write, change functions, then, absolutely, EBS is your knockout winner. Your winner depends on your individual workload. Each service is the right service for specific needs. Once you understand what you need, you will know which service is your champion!


### Amazon Elastic File System (Amazon EFS)

EFS manage file system for shared data access or shared file system.  Multiple EC2 instances can access EFS and EFS scales up and down as need.

EBS vs EFS  
- ESB attaches to an EC2 instance
- AZ level resource need to be in the same AZ - store files, database
- Doesn't scale automatically. 

EFS   
- Multple instances reading and writing to it concurrently
- True file system for Linux
- Regional resource it can work across mutliple AZs
- Automatically scales as needed
- on-prem servers can access EFS via AWS Direct Connect. 




### Transcript
Next up on the list of storage services is Amazon Elastic File System, or what we call EFS. EFS is a managed file system. It's extremely common for businesses to have shared file systems across their applications. For example, you might have multiple servers running analytics on large amounts of data being stored in a shared file system. This data traditionally has been hosted on premises. In this on-premises data center, you would have to ensure that the storage you have can keep up with the amount of data that you are storing. Make sure backups are taken, and that the data is stored redundantly as well as manage all of the servers hosting that data. 


Luckily with AWS, you don't need to worry about buying all of that hardware and keeping the whole file system running from an operational standpoint. With EFS, you can keep existing file systems in place but let AWS do all the heavy lifting of the scaling and the replication. EFS allows you to have multiple instances accessing the data in EFS at the same time. It scales up and down as needed without you needing to do anything to make that scaling happen. Super nice, right? Well, you might be thinking, Amazon EBS also lets me store files that I can access from EC2 instances. What exactly is the difference here?


[Blaine] AWS Cloud Practitioners, welcome back!


[Morgan] All right, we don't need to do all of that. The answer is really simple. Amazon EBS volumes attach to EC2 instances and are an Availability Zone-level resource. In order to attach EC2 to EBS, you need to be in the same AZ. You can save files on it. You can also run a database on top of it. Or store applications on it. It's a hard drive. If you provision a two terabyte EBS volume and fill it up, it doesn't automatically scale to give you more storage. So that's EBS. Amazon EFS can have multiple instances reading and writing from it at the same time.


But it isn't just a blank hard drive that you can write to. It is a true file system for Linux. It is also a regional resource. Meaning any EC2 instance in the Region can write to the EFS file system. As you write more data to EFS, it automatically scales. No need to provision any more volumes.

### Amazon Relation Database Service

Database tables store individual data.  Linked through a common field or key.  Query the databases with SQL.

Supported Databases
- Amazon Aurora 
- MYSQL
- PostgresSQL
- Oracl
- Microsoft SQL

Move RDMS to AWS with lift and shift migration strategy. 

Use Amazon Relational Database System (RDS) as a manage sevice
- patching
- provisioing
- database setup
- backups

Migrate database to Amazon Aurora includes replication and failover.  Replicates 6 copies across 3 AZs and continously backups up data to Amazon S3
- MySQL
- PostgreSQL


#### Transcript
So you're storing data about your coffee shop in various systems. But you're finding that you need to maintain relationships between various types of data. And by relationships, I mean, if say, a customer orders the same drink multiple times, maybe you want to offer them a promotional discount on their next purchase. And you need a way to keep track of this relationship somewhere. In this case, it's best to use a relational database management system, or RDBMS. Essentially, It means we store data in a way such that it relates to other pieces of data. 


For example, if we had a customer entry or record, we store that in a customer table. We then could have an entry for the physical address, which we store on a corresponding address table. We then relate the two via a common attribute and can query the data that is housed in both tables. 


The most common way to query the data is by writing queries in SQL. And this runs on a variety of database systems. Speaking of database systems, what are some of the more well known ones that AWS supports? Well, there's MySQL, PostgreSQL, Oracle, Microsoft SQL Server, and many more. If you have an on-premises environment, you're probably running one of those and they're most likely housed in your data center. 


But is there a way to easily move them to the cloud? Well, the simple answer is yes, you can do what we call a Lift-and-Shift, and migrate your database to run on Amazon EC2. This means you have control over the same variables you do, in your on-premises environment, such as OS, memory, CPU, storage capacity, and so forth. It's a quick entry to the cloud, and you can migrate them using standard practices or using something like Database Migration Service, which we'll cover in a later video. 


The other option for running your databases in the cloud is to use a more managed service called Amazon Relational Database Service, or RDS. It supports all the major database engines, like the ones we mentioned earlier, but this service comes with added benefits. These include automated patching, backups, redundancy, failover, disaster recovery, all of which you normally have to manage for yourself. This makes it an extremely attractive option to AWS customers, as it allows you to focus on business problems and not maintaining databases. Which if you're a database admin, can be pretty time consuming and difficult. 


So how do we make it even easier for you to run database workloads on the cloud? Well, we go one further and have them migrate or deploy to Amazon Aurora. It's our most managed relational database option. It comes in two forms, MySQL and PostgreSQL. And is priced is 1/10th the cost of commercial grade databases. That's a pretty cost effective database. The other benefits are things like your data is replicated across facilities, so you have six copies at any given time. You can also deploy up to 15 read replicas, so you can offload your reads and scale performance. Additionally, there's continuous backups to S3, so you always have a backup ready to restore. You also get point in time recovery, so you can recover data from a specific period. 


And there you have it, relational databases in a nutshell.

### Amazon DynamoDB

#### Transcript
Let's talk about Amazon DynamoDB. At its most basic level, DynamoDB is a database. It's a serverless database, meaning you don't need to manage the underlying instances or infrastructure powering it. 


With DynamoDB, you create tables. A DynamoDB table, is just a place where you can store and query data. Data is organized into items, and items have attributes. Attributes are just different features of your data. If you have one item in your table, or 2 million items in your table, DynamoDB manages the underlying storage for you. And you don't need to worry about the scaling of the system, up or down. 


DynamoDB stores this data redundantly across availability zones and mirrors the data across multiple drives under the hood for you. This makes the burden of operating a highly available database, much lower. 


DynamoDB, beyond being massively scalable, is also highly performant. DynamoDB has a millisecond response time. And when you have applications with potentially millions of users, having scalability and reliable lightning fast response times is important. 


Now, DynamoDB isn't a normal database. In the sense that it doesn't use the very widely used query language, sequel, or SQL. Relational databases, like a standard MySQL Database, require that you have a well defined schema, in place. That might consist of one, or many tables that might relate to each other. You then use SQL to query the data. 


This works great for a lot of use cases, and has been the standard type of database historically. However, these types of rigid SQL databases, can have performance and scaling issues when under stress. The rigid schema also makes it so that you cannot have any variation in the types of data that you store in a table. So, it might not be the best fit for a dataset that is a little bit less rigid, and is being accessed at a very high rate. 


This is where non-relational, or NoSQL, databases come in. DynamoDB is a non-relational database. Non-relational databases tend to have simple flexible schemas, not complex rigid schemas, laying out multiple tables that all relate to each other. 


With DynamoDB, you can add and remove attributes from items in the table, at any time. Not every item in the table has to have the same attributes. This is great for datasets that have some variation from item to item. Because of this flexibility, you cannot run complex SQL queries on it. Instead, you would write queries based on a small subset of attributes that are designated as keys. 


Because of this, the queries that you run are non-relational databases tend to be simpler, and focus on a collection of items from one table, not queries than span multiple tables. This query pattern, along with other factors, including the way that the underlying system is designed, allows DynamoDB to be very quick in response time, and highly scalable. 


So, things to remember: DynamoDB is a non-relational, NoSQL database. It is purpose built. Meaning it has specific use cases, and it isn't the best fit for every workload out there. It has millisecond response time. It's fully managed, and it's highly scalable. One awesome example is on Prime Day in 2019, across the 48 hours of Prime Day, there were 7.11 trillion calls to the DynamoDB API, peaking at 45.4 million requests per second. That's insanely scalable, all without the underlying database management. That's pretty cool.
