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

# AWS-EB-CLI

For this step, I am setting up Elastic Beanstalk for the application I'm running. Here are the steps involved:

1. **Set Up AWS Elastic Beanstalk Credentials:**
   - First, I set up credentials for AWS Elastic Beanstalk. These credentials will allow us to interact with Elastic Beanstalk from the command line.

2. **Change Directory to Application File:**
   - Once the AWS Elastic Beanstalk credentials are set up, we change our terminal's working directory to our application's file location. This is where we have our application code.

3. **Configure Elastic Beanstalk:**
   - Within the application directory, I configure Elastic Beanstalk settings, including:
     - Defining the AWS region for the Elastic Beanstalk instance.
     - Specifying the application name.
     - Selecting the Python version in which the application should run.
     - Setting up security groups, load balancers, and auto-scaling groups as necessary.

## Addition to Jenkins

I added the following stage to my Jenkinsfile, which is the 'deploy' stage:

```groovy
stage ('Deploy') { 
    steps { 
        sh '/var/lib/jenkins/.local/bin/eb deploy' 
    } 
}

```
This stage was added towards the end of the Jenkinsfile, and it adds the "deploy" stage to the Jenkins pipeline.

# Webhook

## Webhook Configuration

This step involved the creation and configuration of a webhook. We used our EC2 Public IP to set up the webhook in a way that, if anything was changed in the GitHub Repository, it would automatically trigger a push to Jenkins for testing. This automated process even further

## Bonus: Automatic Deployment

As an added bonus, once the webhook was configured, I made a specific change to the `home.html` file on GitHub. I changed a URL label to “Type something here.” With the webhook in place, this change triggered an automatic deployment into Jenkins.

After the change ran successfully on Jenkins and the testing was complete, the changes were pushed onto the actual application.



