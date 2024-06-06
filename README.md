
Jenkins server: A Jenkins server is an automation tool used for continuous integration (CI) and continuous delivery (CD) in software development. It helps automate the process of building, testing, and deploying code changes, ensuring that code quality is maintained and deployment is consistent. Jenkins integrates with various tools and platforms through plugins, supports defining workflows as code, and can scale across multiple machines to handle large workloads. It is widely used to improve development efficiency and ensure early detection of issues.
setup:
1. Install the required version of java as jenkins is built in java and run on Java Virtual Machine (JVM)
    1. sudo apt update
    2. sudo apt -get install openjdk-17-jdk
   
    ![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/c01b7211-ebb6-47fb-8871-4a9954220068)
   
2. Install jenkins
    1. sudo apt install apt-transport-https -y
    2. wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo apt-key add -
    3. sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    4. sudo apt update
    5. sudo apt install jenkins -y
    6. sudo systemctl start jenkins
    7. sudo systemctl enable jenkins
    and the jenkins server is exposed on port 8080 by default. Make sure to keep the port open on the virtual machine and on firewall if any
   
   ![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/685691ab-91d0-4b55-9644-a64d40d6cab1)
   
   retrieve the password from the given file, proceed with installation of required plugins, and create first admin user.
   
   ![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/63a27b55-b43a-4414-80e2-01189d9d880f)

3. Install Docker on the same jenkins server which we use as an agent for running the pipelines.
    1. sudo apt-get update
    2. sudo apt-get install ca-certificates curl
    3. sudo install -m 0755 -d /etc/apt/keyrings
    4. sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    5. sudo chmod a+r /etc/apt/keyrings/docker.asc
    6. echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    7. sudo apt-get update
    8. sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/3b500ba5-53ad-458b-bb86-69afb39809cc)
    to enable any user like jenkins user to run the docker commands as the root user, like creating containers, deleting containers, etc.
    ![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/869cae3c-fadf-4474-842c-9336eaff5dff)

Install the below mentioned plugins . go to manage jenkins -> plugins -> available plugins
1. eclipse temurian installer (for installing and using the required version of jdk on agent)
2. config file provider (required to create a maven setting.xml file for deploying the build artifact to the nexus repository)
3. sonarqube-scanner (tool to perform automatic code review)
4. docker
5. docker pipeline
6. kubernetes
7. kubentetes CLI
8. pipeline maven intgration
9. maven integration
to use the third-party tools installed as plugins in the jenkins pipelines, Configure the installed plugins as tools in manage jenkins -> tools
![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/c79dfd71-ef86-4a5e-baea-ec333f80c62d)
![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/5e50bcdd-d374-43f1-a251-2eecd60e32cc)
![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/4b1e0c71-063f-4a50-ad76-5de8442f4eac)
![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/d285e870-40c7-48bc-8730-c223e7b7a71b)


SonarQube:SonarQube is an open-source platform used for continuous inspection of code quality through static code analysis, detecting bugs, code smells, and security vulnerabilities across more than 25 programming languages. It provides detailed metrics and reports, integrates seamlessly with CI/CD tools like Jenkins, and allows customization of coding rules to enforce standards. By using SonarQube, development teams can improve code quality, maintainability, and security, receive continuous feedback, and ensure compliance with coding best practices, making it an essential tool for maintaining high standards in software development projects.

Sonarqube-scanner plugin performs the code quality analysis, generates the reports, and publish the reports to the configured sonarqube server.

setup: (running the sonarqube server on the same jenkins server as a docker container and publishing the service on port 9000 of the host)
![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/14e01a58-5c9d-4b53-9dcc-9a15f61d6e68)
![image](https://github.com/venkatesh-reddy679/Board_Game-CI-CD/assets/60383183/efbbf27c-0e65-4951-900f-b7a78574644a)
default username: admin && default password: admin










 


   

