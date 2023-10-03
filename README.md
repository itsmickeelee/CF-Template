# CF-Template
Description: Template to create an EC2 instance and enable SSH

Parameters: 
  KeyName:
    Description: Name of SSH KeyPair
    Type: 'AWS::EC2::KeyPair::KeyName'
    ConstraintDescription: Provide the name of an existing SSH key pair

Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0bdb1d6c15a40392c
      KeyName: !Ref KeyName
      SecurityGroups:
       - Ref: InstanceSecurityGroup
      Tags:
        - Key: Name
          Value: My CF Instance
  InstanceSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
        IpProtocol: tcp
        FromPort: 22
        ToPort: 22
        CidrIp: 0.0.0.0/0

Outputs: 
  InstanceID:
    Description: The Instance ID
    Value: !Ref MyEC2Instance
