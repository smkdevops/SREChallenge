# SREChallenge

#-----------------------------------------------------SRE Challenge------------------------------------------------

#Create and deploy a running instance of a web server using a configuration management tool of your choice. The web server should serve one #page with the following content.
#<html>
#<head>
#<title>Hello World</title>
#</head>
#<body>
#<h1>Hello World!</h1>
#</body>
#</html>
#Secure this application and host such that only appropriate ports are publicly exposed and any http requests are redirected to https. This #should be automated using a configuration management tool of your choice and you should feel free to use a self-signed certificate for the #web server.

#Develop and apply automated tests to validate the correctness of the server configuration.

Step1: 

EC2 Instance provisioning in us-west-2 region with Ansible as configuration Management tool. 

Here the playbooks location https://github.com/smkdevops/SREChallenge/blob/master/ansible_aws_ec2_provisioning that provision the ec2 instances to configure and deploy our application

Here i have added Ansible playbooks as well to configure the web server environment. 

Step2: 

Test Kitchen and Vagrant can be configured in our local CHEF workstation that we can use to test and implement chef recipes. But to verify that a cookbook's recipes will run correctly in production, we must run them on an AWS OpsWorks Stacks instance.

Here the CHEF recipes we can use to AWS OpsWorks Stacks to quickly configure a Apache application environment. https://github.com/smkdevops/SREChallenge/blob/master/Chef-Apache-Recipe.zip

aws opsworks create-stack --name "CLI Stack" --stack-region "us-east-1" --service-role-arn arn:aws:iam::123456789012:role/aws-opsworks-service-role --default-instance-profile-arn arn:aws:iam::123456789012:instance-profile/aws-opsworks-ec2-role --region us-east-1

aws opsworks --region ap-south-1 create-deployment --stack-id 935450cc-61e0-4b03-a3e0-160ac817d2bb --command "{\"Name\":\"execute_recipes\", \"Args\":{\"recipes\":[\"nginx::application\"]}}

Step 3:

ChefSpec -> A Unit Test framework that tests chef resources locally. 

ChefSpec tests for the apache cookbook 

chef exec rspec 

This will run based on [spec/unit/recipes/default_spec.rb] defined under https://github.com/smkdevops/SREChallenge/blob/master/Chef-Apache-Recipe.zip

Step 4: 

InSpec - Integration testing framework for chef recipes. 

kitchen converge

Kitchen verify 

This will ensure your changes are converged on your test instance

Step 5: Monitor the Environment: 

Amazon cloutwatch uses to monitor AWS opsworks & detailed monitoring for each instance in the stack.

We can integrate AWS cloudtrail to log every AWS OpsWorks Stacks API call and store the data in an Amazon S3 bucket. 

we can use Amazon CloudWatch Logs to monitor your stack's system & application.









-
  
