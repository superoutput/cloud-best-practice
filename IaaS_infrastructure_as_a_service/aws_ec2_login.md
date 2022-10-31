# EC2 Access

There are 3 ways to login to an Amazon EC2 Linux instance:

#### SSH

When the Amazon EC2 instance is launched, select a keypair that is already loaded into AWS. When the instance launches, the public half of the keypair will be copied into the `~/.ssh/authorized_keys` file for the `ec2-user`.

You can then login to the instance using the private keypair:

```shell
ssh -i keypair.pem ec2-user@1.1.1.1
```

#### EC2 Instance Connect

EC2 Instance Connect has two features:
- The ability to push a 'temporary keypair' to the EC2 instance
- The ability to establish an SSH connection via a web browser

Permission can be granted to an IAM User to use EC2 Instance Connect. Therefore, a user can login to the EC2 instance by using their AWS credentials. They are effectively requesting a connect via EC2 Instance Connect, and all the SSH stuff is done in the background.

#### AWS Systems Manager Session Manager

Amazon EC2 instances launched with Amazon Linux have an SSM Agent installed. This agent 'calls back' to AWS and offers the ability to use **Session Manager** to login to the instance. This isn't an SSH connection -- rather, it is a connection to the Agent, which runs commands in an interactive session.

Session Manager offers the ability to connect to **instances in private subnets** because the Agent is creating an *outbound* connection to AWS. (The other two methods above cannot be used to connect to an instance in a private subnet).

The ability to use Session Manager is based on permissions of the IAM User.

## References
https://stackoverflow.com/questions/73243470/how-to-connect-to-ec2-instance-using-access-key-id-and-secret-access-key