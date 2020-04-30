# Integration of sonarqube in jenkins

## Prerequisites
Jenkins server \
SonarQube server

## Install 
Install SonarQube Scanner plugin in jenkins 

## Setup Jenkins
Go to Menage jenkins --> Configure System --> SonarQube servers section
Give Name and Server URL and get Server authentication token from sonarqube, and add as secret text
in global credentials
## Setup SonarQube
Go to security section and generate the token which will be use to authenticate 
Jenkins server. \
Create project and assign token key to this project 

You can add this stage in jenkins pipeline 
```
stage("Sonar Scan") {
    steps {
        script {
            def scannerHome = tool 'sonarqube-scanner'
                withSonarQubeEnv ('sonarqube') {
                     sh """
                     ${scannerHome}/bin/sonar-scanner -X -Dsonar.projectKey='apple' -Dsonar.projectName='apple' -Dsonar.projectVersion='1.0.1'
                     """
                }
            }
        }
    }

```