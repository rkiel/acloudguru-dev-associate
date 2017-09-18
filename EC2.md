
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
