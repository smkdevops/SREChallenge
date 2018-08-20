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





Ansible for ec2 provisioning in AWS environment 

CHEF to configure and deploy the web server with Hello world content display. 

https://docs.aws.amazon.com/opsworks/latest/userguide/workinglayers-static.html


ChefSpec tests for the application cookbook 


-----------------------------Create Chef Code to Satisfy the Tests

Create InSpec Integration Tests

['net-tools', 'httpd'].each do |pkg|
  describe package(pkg) do
    it { should be_installed }
  end
end

describe user('webadmin') do
    it { should exist }
    its('group') { should eq 'developers' }
end 

describe group('developers') do
    it { should exist }
end 

  
