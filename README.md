# Week 6 – AWS	Production Environment 	

-	S3 service is a storage

-	EC2 service allows you to create a vm

-	IAM service – creates credentials

-	VPC – creates a virtual cloud for networking

## EC2

The location of this is important as different servers serve different purposes around the globe.

-	Running instances

-	Launch instance

-	Different distributions are available to use. (Use the free tier ones)

-	Different processors to choose from. (We chose the t2. Micro)

-	Configuring instance details (auto assign public ap = enable)

-	Adding storage (how much storage do you want for the machine)

-	Add tag > add a new tag (key: name, value: Kajal-Patel-eng48-first-instance}

-	Configure security group (allows you to configure what you can do from what IP)
o	Port 22 – communicates through ssh, do not have the ssh open to the world so change the source to my IP

-	You can select existing security groups as they have been set up and creating a new group can have many rules.

-	In the Launch tab, key pair is about linking public and private keys stored.
o	When creating a new key, it will download a key and you would want to put it where all the other keys are stored.

	 **C:\Users\Kajal Patel\.ssh**

## Need to ssh into the connection you made and need a terminal:
-	Check on your machine in the terminal you have the ssh key

-	ssh -i ~/< key name > ubuntu@ <IPV4 public IP >
o	eg . ssh -i ~/.ssh/kajal-eng-48-first-key.pem ubuntu@63.32.98.117


## You need to provision the machine:

-	atom. into the starter code given

-	the provision scripts in environment/ app and db there are 2.

-	Check that both the provision scripts have executable writes by cd into them and using the command **ll**

-	db provision didn’t so you need to add the write to execute.

-	**dos2unix -h** to check if u have dos2unix, if not then download it and place the dos2unix in the path in this case it is **(C:\Windows\System32)**

-	cd back into environment/app and use the command **dos2unix <provision file name>**  do the same for db provision.

````
secure copy is a command line tool is linux to copy files between your computer and your instance created on AWS.
````

## How to copy a file

-	scp -i path/to/key file/to/copy user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/file/ <name of provision file>
````
  eg . scp -i ~/.ssh/kajal-eng-48-first-key.pem ../environment/app/provision.sh ubunutu@ 63.32.98.117:/home/ubuntu/file.sh
````

-	go into your ubuntu machine/environment check if the path created the file correctly and then run the provision

to run the file: **./<name of provision file>**

## How to copy a directory

To copy an entire directory, add the -r recursive option: scp -i path/to/key -r directory/to/copy user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/directory.

````
Eg . scp -i ~/.ssh/kajal-eng-48-first-key.pem -r ../environment/ ubuntu@63.32.98.117:/home/ubuntu/
````

-	go into your ubuntu machine/environment check if the path created correctly and then run the provision

  to run the file: **./<name of provision file>**

## How to change the rights of a file

if a provision file is not executing you may not have the rights to do this. So either on your local machine or on your vm you need to go into the path where the .sh provision file is stored and run this command:

**chmod +x <provision file name>**

the x is for executable, it adds the right to execute, you can do this for read and write too.
.
