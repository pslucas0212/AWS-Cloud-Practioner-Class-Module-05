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

#### Transcript
Welcome to this video on Amazon Simple Storage Service, or S3. From the name, you've probably guessed that it is a storage service and it's, well, simple. Most businesses have data that needs to be stored somewhere. For the coffee shop, this could be receipts, images, Excel spreadsheets, employee training videos, and even text files, among others. Storing these files is where S3 comes in handy because it is a data store that allows you to store and retrieve an unlimited amount of data at any scale. 


Data is stored as objects, but instead of storing them in a file directory, you store them in what we call buckets. Think of a file sitting on your hard drive, that is an object and think of a file directory, that is the bucket. The maximum object size that you can upload is five terabytes. You can also version objects to protect them from accidental deletion of an object. What this means is that you always retain the previous versions of an object, as like a paper trail. You can even create multiple buckets and store them across different classes or tiers of data. You can then create permissions to limit who can see or even access objects. 


And you can even stage data between different tiers. These tiers offer mechanisms for different storage use cases such as data that needs to be accessed frequently, versus audit data that needs to be retained for several years. Let's go through the notable ones, shall we? 


The first here is called S3 Standard and comes with 11 nines of durability. That means an object stored in S3 Standard has a 99.999999999 percentage – that's a lot of nines –  probability that it will remain intact after a period of one year. That's pretty high. Furthermore, data is stored in such a way that AWS can sustain the concurrent loss of data in two separate storage facilities. This is because data is stored in at least three facilities. So multiple copies reside across locations. Another useful way to use S3 is static website hosting, where a static website is a collection of HTML files and each file is akin to a physical page of the actual site. You can do this by simply uploading all your HTML, static web assets, and so forth into a bucket and then checking a box to host it as a static website. You can then enter the bucket's URL and ba-bam! Instant website. And we say static, but that doesn't mean you can't have animations and moving parts to your website. Pretty awesome way to start up that coffee blog. 


The next storage class is called S3 Infrequent Access or S3-IA. Which is used for data that is accessed less frequently but requires rapid access when needed. This means it's a perfect place to store backups, disaster recovery files, or any object that requires a long-term storage. 


Another storage class or tier lends itself to that example we had earlier about audit data. Say, we need to retain data for several years for auditing purposes. And we don't need it to be retrieved very rapidly. Well, then you can use Amazon S3 Glacier to archive that data. To use Glacier, you can simply move data to it, or you can create vaults and then populate them with archives. And if you have compliance requirements around retaining data for, say, a certain period of time, you can employ an S3 Glacier vault lock policy and lock your vault. You can specify controls such as write once/ read many, or WORM, in a vault lock policy and lock the policy from future edits. Once locked, the policy can no longer be changed. You also have three options for retrieval, which range from minutes to hours, and you have the option of uploading directly to Glacier or using S3 Lifecycle policies. 


Fact, I don't think we mentioned lifecycle policies up till this point. But they are policies you can create that can move data automatically between tiers. For example, say we need to keep an object in S3 Standard for 90 days, and then we want to move it to S3-IA for the next 30 days. Then after 120 days total, we want it to be moved to S3 Glacier. With Lifecycle policies, you create that configuration without changing your application code and it will perform those moves for you automatically. It's another example of a managed AWS service, helping take that burden off you, so you can focus on more of your business needs. 


Just to note that there are other storage classes. Like S3 Infrequent Access One Zone and S3 Glacier Deep Archive that you can use. Happy storing.

