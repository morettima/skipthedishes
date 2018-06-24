My main goal its to show how to use a pipeline from github to jenkins (this one build a server and deploy changes etc, to test and production in automated way) using aws codedeploy
**The number at left its about some screenshots.

    //create aws new account
    //create basics account, roles (important one about JenkinsAccess), groups...
    //configurate JenkinsAccess in roles.
1.  //create one instance to install jenkins
    //Start to install jenkins
    sudo yum update
    [y]
    sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
    [y] 
    sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
    sudo yum install jenkins
    [y]
    sudo chkconfig jenkins on
    sudo service jenkins status // just for testing, result : jenkins is stopped
    sudo service jenkins start // found error from java, need at least version 8
    sudo yum remove java
    [y]
    sudo yum install java-1.8.0-openjdk
    [y]
    java -version  // result ok : openjdk version "1.8.0_171" 
                                  OpenJDK Runtime Environment (build11   1.8.0_171-b10)
                                  OpenJDK 64-Bit Server VM (build 25.171-b10, mixed mode)
    sudo service jenkins start // result ok : Starting Jenkins             [  OK  ]
    //i just disable the firewall to get some time, normal days configurate in iptables right roles...
    sudo service iptables save
    sudo service iptables stop
    sudo chkconfig iptables off
3.  // add new roles aws to allow 8080 from anywhere.
2.  // Starting using jenkins web man.
4.  // Then I go to manage jenkins, manage plugins
5.  // search for aws codepipeline, install and reboot.
6.  // new job, myproject and select free-style.
    aws --version  //check if aws cli its ok.
    pip install awscli --upgrade --user // found version 9, and have already version 10
    pip install --upgrade pip  // make the upgrade
7.  // On configuration page, check execute concurrent builds if necessary and choose, aws, make sure your region its right.
8.  // type your provider name, and inside build triggers, schedule, make like crontab, and choose your frequency you want.
9.  // Execute build, put rake, and choose aws codepipeline publisher, leave the rest blank. Save, this part its done.
    sudo yum install rake // at this point i remember rake isnt default program, so i login via ssh and install.
10. //  Now we are going to aws management console, in codepipeline module. to create a new one. Give a name.
11. //  Provider, select github, click to link your/desired account.
12. //  Authorize.
13. //  Then select with repo and branch you want.
14. //  Add provider Jenkins, use same provider name you use before, and your link 
14. //  I took the screenshot before put right link : ec2-18-231-184-2.sa-east-1.compute.amazonaws.com:8080
14. //  In review screenshot (number 16) show correct link.
15. //  Deploy menu : Choose your pipeline from aws. or create a new one. this case i use this one :aws codedeploy
15. //  In the next two lines, use refresh, and choose the option you want (in my case have only one of each, but you can have more than one...)
16. //  Choose the service role we created before. aws-codepipeline-service
17. //  Review with caution to see if everything is correct. And create the pipeline
18. //  Pipeline created.
19. //  Logs ok!

    
    
    
