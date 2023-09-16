<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>

# Webhook Flask

This project showcases the use of Jenkins to automate the testing stages of a deployment. While also allowing the user to create commands to install Python and AWS Elastic Beanstalk into an EC2 server.

## Planning

### Installing Jenkins & Python

I started off by installing Jenkins into my EC2 server by using a series of commands:

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install fontconfig openjdk-11-jre
sudo apt-get install Jenkins
```
Once Jenkins was installed. Python needed to be installed with the command “sudo install python3.10-ven”. Also had to install “python-pip” and “unzip”.
Once everything is installed, we head over to the Jenkins server using the Public IP address from our EC2 instance. We created a multibranch pipeline on Jenkins using the GitHub repository the application files are in and added credentials to it. When deployed the application ran successfully. 

![image](https://github.com/Jmo-101/Web_Hook_Flask/assets/138607757/8296eb60-e9da-41a5-9ead-c60513bd86be)


