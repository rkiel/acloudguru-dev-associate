
# EC2 - [back](README.md)

#### Connecting via SSH

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
