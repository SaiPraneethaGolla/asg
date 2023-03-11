# asg
AWSTemplateFormatVersion: "2010-09-09"
Description: Create launch template and Autoscaling Group.

Parameters:
  LaunchTemplateVersionNumber:
    Default: 1
    Type: String

Resources:
  MyLaunchTemplate:
    Type: AWS::EC2::LaunchTemplate
    Properties:
      LaunchTemplateName: Template-1
      LaunchTemplateData:
        ImageId: ami-0d81306eddc614a45
        InstanceType: t2.micro
        KeyName: batch10
        SecurityGroupIds:
          - sg-05f87e8f63010da41

  ASG1:
    Type: AWS::AutoScaling::AutoScalingGroup
    Properties: 
      AutoScalingGroupName: Batch11ASG
      VPCZoneIdentifier:
          - subnet-06dd1f259fe362a7d
          - subnet-0d565caec776dc84b   
      DesiredCapacity: 2
      MaxSize: 3
      MinSize: 1
      LaunchTemplate:
        LaunchTemplateId: !Ref MyLaunchTemplate
        Version: !Ref LaunchTemplateVersionNumber    
