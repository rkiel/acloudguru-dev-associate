
# EC2 - [back](README.md)

#### Connecting via SSH

Set key pair permissions

```bash
chmod 400 MyEC2KeyPair.pem
```

Connect

```bash
ssh ec2-user@111.222.333.444 -i MyEC2KeyPair.pem
```

#### Updating an new EC2 instance

```bash
sudo yum update -y
```

#### Installing Apache

```bash
sudo su
yum install httpd -y
service httpd start
chkconfig httpd on
cd /var/www/html
vim index.html
exit
```

#### Sample `index.html`

```html
<html>
  <body>
    <h1>Hello Cloud Gurus<h1>
  </body>
</html>
```

#### Configure AWS CLI
* Credentials stored in `~/.aws/credentials`
* Configuration store in `~/.aws/config`

```bash
aws configure
```

#### Creating/launching a new EC2 instance

```bash
aws ec2 run-instances \
  --image-id ami-00000 \
  --count 1 \
  --instance-type t2.micro \
  --key-name MyEC2KeyPair \
  --security-group-ids sg-1111111  \
  --subnet-id subnet-222222
  ```

#### All current running

```bash
aws ec2 describe-instances
```

#### Catalog of thousands

```bash
aws ec2 describe-images
```

#### Instance Metedata

* [Instance Metadata and User Data](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)

To view all categories of instance metadata from within a running instance, use the following URI:

```bash
curl http://169.254.169.254/latest/meta-data/
```

To view a specific instance metadata, for example:

```bash
curl http://169.254.169.254/latest/meta-data/public-ipv4
```

#### Elastic Load Balancer

[Read the FAQ -- especially the Class LB](https://aws.amazon.com/elasticloadbalancing/faqs/)

* virtual appliance to spread the load of your traffic across you web servers
    1. **Application LB** -- Layer 7 and the preferred for HTTP/HTTPS
    1. **Classic LB** -- Layer 4 for TCP/SSL
* Application is new and probably won't be on the exam
* Advanced details
    * **Response timeout** -- time to wait when receiving a response from a health check (2-60 sec)
    * **Interval** -- amount of time between health checks (5-300 sec)
    * **Unhealthy threshold** -- number of consecutive health check failures before declaring an EC2 instance unhealthy (2-10)
    * **Healthy threshold** -- number of consecutive health check successes before declaring an EC2 instance health (2-10)
* You do NOT get a public IP; just a DNS name
* Instances monitored by ELB are reported as InService or OutOfService
* Health Check checks the instance health by talking to it
* Have their own DNS name.  You are never given an IP address

#### SDK Exam Tips

[Tools](https://aws.amazon.com/tools/)

Languages

* Android, iOS, Browser (JavaScript)
* Java
* .Net
* Node.js
* PHP
* Python
* Ruby
* Go
* C++

Regions

* some SDKs have a default region: `us-east-1`
    * i.e. Java does and Node.js does not

#### Summary & Exam Tips

[EC2 Documentation](https://aws.amazon.com/ec2/) | [Storage](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Storage.html) | [FAQ](https://aws.amazon.com/ec2/faqs/)

* Know the difference between On Demand, Spot, Reserved, Dedicated Hosts
    * choose the best pricing model for the scenario
* Spot Instances
    * You terminate, you pay for the full hour; AWS terminate, you don't pay for the partial hour
* DR MCGIFT PX
* EBS
    * SSD GP2, SSD IO1, HDD ST1, HDD SC1, HDD Standard
    * cannot be mounted to multiple EC2 instances;  use EFS instead
* Termination Protection is turned off (by default)
* Root EBS volume will be deleted on termination (by default)
* Root EBS volume cannot be encrypted (by default)
* Additional EBS volumes can be encrypted (by default)
* Volumes
    * exist on EBS
    * you can take a snapshot of a volume
    * volumes restored from encrypted snapshot are encrypted automatically
* Snapshots
    * exist on S3
    * point in time copies of a volume
    * incremental; only blocks that have changed are moved to S3
    * first snapshot will take time to create
    * snapshots of encrypted volumes are encrypted automatically
    * can be shared but only if they are unencrypted
    * share with other AWS accounts or make them public
    * snapshot of a root volume you should stop the instance first
* Instance Store volumes (Ephemeral Storage)
    * cannot be stopped
    * lose data if host fails
    * you can reboot and not lose data
* AMI
    * they are regional
    * can only launch an AMI from the region in which it is stored
    * but they can be copied to other regions
* CloudWatch
    * for performance monitoring
    * standard monitoring -- 5 min; detailed monitoring -- 1 min
    * dashboards to see what's going on
    * alarms to notify you when something happens
    * events to respond to state changes
    * logs to aggregate, monitor and store logs
* CloudTrail
    * for auditing
* Roles
    * more secure than having you access key id & secret key
    * easier to manage
    * can now be assigned after an EC2 instance is provisioned
    * policies can be added/removed which are effective immediately
    * universal and can be used in any region
* Instance meta-data
    * no such thing as user-data for an instance
* EFS (beta only in Oregon)
    * supports NFS
    * only pay for what you use
    * can scale up to petabytes & thousands of connections
    * data stored across multiple availability zones
    * read after write consistency
* Lambda
