# LEMP Stack by Cloudeya Setup

A Cloudeya image includes everything you need to run your Cloudeya-packaged application of choice. The installation and configuration of all of the software included in the stack is completely automated, making it easy for everyone, including those who are not very technical, to get them up and running.

All Cloudeya images are completely self-contained and run independently of the rest of the software or libraries installed on your system. This means that you don’t have to worry about installing any other software on your system to make the new application work. They also won’t interfere with any software already installed on the system, so everything will continue to work normally.

## Preliminary Setup

You need to create a unique EC2 Key Pair so you can log into your EC2 instance easily. Within the AWS Management Console:

1. Go to **EC2** > **Network & Security** > **Key Pairs**
2. Click **Create Key Pair**
3. Enter a Key pair name and click **Create**
4. Download your Key pair with a **.pem** extension and store it in a safe place on your computer.

## Launch Instance

Within the EC2 Dashboard page, you can do the following to launch an LEMP Stack by Cloudeya instance:

1. Click the **Launch Instance** button or click this button [![Launch Stack](./images/launch-stack.png?raw=true)](https://aws.amazon.com/marketplace/pp/B08S71PRTS)
2. Next, click **AWS Marketplace** tab on the left side of the **Choose an Amazon Machine Image (AMI)** page
3. Enter the phrase **lemp stack by cloudeya** in the search box and press **enter** on your keyboard
4. Click the **select** button in front of LEMP Stack by Cloudeya
5. Click the **continue** button in the dialog box
6. Select an instance type that fits your budget then click the **Review and Launch** button
7. Configure these options (**Security Groups**, **Instance Details**, **Storage**, and **Tags**) to match your business needs
8. Click the **launch** button

## Connect To The Server Using SSH

To SSH into your EC2 instance:

1. ```cd``` to the location of your .pem key
2. Run ```chmod 600 mykey.pem``` to lock down your SSH key
3. Run ```ssh -i /path/my-key-pair.pem ec2-user@<your ip address>``` ## Amazon Linux 2 Version
4. Run ```ssh -i /path/my-key-pair.pem ubuntu@<your ip address>``` ## Ubuntu Version
5. Bam!!! Have fun. Don't break anything, but if you do. Support is available [here](mailto:tech@cloudeya.org).

## Where is MySQL Password?

To SSH into your EC2 instance:

1. Type ```sudo su -``` in terminal after SSH into your EC2 instance
2. ```cat /var/log/mysql_password.log``` to reveal your MySQL root password

## How change MySQL Password?

1. Start MySQL/MariaDB without grant tables option.This will allow us to login to MySQL/MariaDB as a root user without a password

```bash
$ sudo service mysql stop
$ sudo mkdir -p /var/run/mysqld
$ sudo chown mysql:mysql /var/run/mysqld
$ sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
```

2. Confirm that the MySQL/MariaDB daemon is up and running

```bash
ps aux | grep mysqld
```

3. At this point, login to MySQL/MariaDB should not require any password

```bash
mysql -u root
```

Execute the following SQL commands to reset your administrator password

```bash
## The password below is precisely for this documentation; it's invalid.
## The password in your Amazon Machine Image (AMI) will be unique.

FLUSH PRIVILEGES;
USE mysql; 
ALTER USER 'root'@'localhost' IDENTIFIED BY 'mYN3w_p@ssw0rD$';
quit
```

4. Restart the MySQL/MariaDB server

```bash
sudo pkill mysqld && sudo systemctl start mysql
```

5. At this point you should be able to login to the MySQL/MariaDB server with the password as set in the step 3

```bash
## The password below is precisely for this documentation; it's invalid.
## The password in your Amazon Machine Image (AMI) will be unique.

mysql -u root --password='mYN3w_p@ssw0rD$'
```

## Links

1. [Product Page](https://aws.amazon.com/marketplace/pp/prodview-razaxxxuz26z6)
2. [EULA](CloudeyaLimitedEULA.txt)
3. [Knowledgebase](https://github.com/cloudeyalimited/lemp-stack-by-cloudeya/-/wikis/home)
4. [Issue Tracking](https://github.com/cloudeyalimited/lemp-stack-by-cloudeya/-/issues)
5. [Changelog](changelog.md)

## Support

[Email](mailto:tech@cloudeya.org) support is available to Amazon Web Services Marketplace Customers. We do not offer refunds, but you may terminate your LEMP Stack by Cloudeya at any time.

## License

The documentation is published under [BSD 3-Clause License](license.txt).

## Copyright

(c) 2020 - 2024 [Cloudeya Limited](https://cloudeya.org).
