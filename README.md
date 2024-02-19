# AWS_Use-Cloud-Formation-to-Launch-EC2-Web-Server

**Use Cloud Formation to Launch an Amazon EC2 Web Server**


Following the steps you should follow

Step 1: Search Cloud Formation <br><br>
Step 2: Click on Create Stack.<br><br>
Step 3: We can see Prereuisite - prepare template.<br><br>
Step 4: Select your template.<br>
      1. Template is ready.<br>
      2. Use a sample template.<br>
      3. Create template in Designer.<br>
<i><b>Here we select Template is ready.</b></i><br><br>
Step 5: Then we select Specify template.<br>
      1. Amazon S3 URL.<br>
      2. Upload a template file.<br>
<i><b>Here we select Template is ready.</b></i><br><br>
Step 6: Click on choice file.<br><br>
Step 7: Then select your yml file.<br>
In this file, we just checked our CloudFormation.<br>
and in this file, I write code.<br>

## Example Code:

```
---
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-a4c7edb2
      InstanceType: t2.micro 
```

Step 8: Open a terminal.<br><br>
Step 9: Create a new file and paste this code there.<br>
To create a new file in Windows, use the "Start notepad yourfilename.yml" command.<br>
**Note**: Your extension must be. yml<br><br>
Step 10: Then save that file and write ":wq"<br><br>
Step 11: Then click on "View in Designer."<br><br>
Step 12: Click on Next. <br><br>
Step 13: Enter the name of the stack.<br><br>
Step 14: Before this, we should select our region. <br><br>
Step 15: Click on Next.<br><br>
Step 16: In tags, we add some tags up to 50.<br><br>
Step 17: In permission (select the default one)<br><br>
Step 19: In Stack failure options (select the default one)<br><br>
Step 20: In the Advanced option (select the default one),<br>
      1. Stack policy (select the default one)<br>
      2. Rollback configuration (select the default one)<br>
      3. Notification option (select the default one)<br>
      4. Stack creation options (select the default one)<br><br>
Step 21: Click on Next.<br><br>
Step 22: Now we can see our stack. <br><br>
Step 23: Now we open EC2 (go to the search bar and type).<br><br>
Step 24: We can check if our instance is running.<br><br>
Step 25: Then in Cloud Formation -> Stacks -> Your Stack, we can see some lists like Stack info, Events, Resources, Output, Parameters, templates, and Change sets.<br><br>
Step 26: So that in Template we can see our template we implemented in our instance<br><br>
Step 27: If you want to update the template, just click Update and change your file. <br>
**Note**: We use other code in the yml file. <br><br>
Step 28: Click on choice file<br><br>
Step 29: Then select your yml file. <br><br>
In this file, we just checked our CloudFormation. <br>
and in this file, I write code.<br>

## Full Code:

```
---
Parameters:
  SecurityGroupDescription:
    Description: Security Group Description
    Type: String

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-a4c7edb2
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref SSHSecurityGroup
        - !Ref ServerSecurityGroup

  # an elastic IP for our instance
  MyEIP:
    Type: AWS::EC2::EIP
    Properties:
      InstanceId: !Ref MyInstance

  # our EC2 security group
  SSHSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
      - CidrIp: 0.0.0.0/0
        FromPort: 22
        IpProtocol: tcp
        ToPort: 22

  # our second EC2 security group
  ServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: !Ref SecurityGroupDescription
      SecurityGroupIngress:
      - IpProtocol: tcp
        FromPort: 80
        ToPort: 80
        CidrIp: 0.0.0.0/0
      - IpProtocol: tcp
        FromPort: 22
        ToPort: 22
        CidrIp: 192.168.1.1/32

Outputs:
  ElasticIP:
    Description: Elastic IP Value
    Value: !Ref MyEIP
```

Step 30: Open terminal. <br><br>
Step 31: Create a new file and paste this code there.<br><br>
Step 32: We can also see these on "View in Designer."<br><br>
Step 33: Click on Next.<br><br>
Step 34: Enter the name of the security group<br><br>
Step 35: Click on Next.<br><br>
Step 36: You should not change other settings. <br><br>
Step 37: Click on Next.<br><br>
Step 38: If you want to verify this, just go to the EC2 instance.<br><br>
Step 39: In the ablove code, we just change the file of Cloud Formation, so in the example code instance created, we change it to Full code so it's automatically terminate that instance<br>
