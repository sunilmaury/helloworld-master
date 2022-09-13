pipeline {
    agent any
    tools {
        maven "Maven"
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "maven-repo"
        NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
    }
    stages {
        stage("Clone code from Git Repo") {
            steps {
                script {
                    git 'https://github.com/sunilmaury/helloworld-master.git';
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh "mvn clean install"
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps{
                
                 nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'maven-project', 
                        classifier: '',
                        file: 'C:/ProgramData/Jenkins/.jenkins/workspace/hello-world/webapp/target/webapp.war',
                        type: 'war'
                    ]
                ], 
                credentialsId: 'nexus-user-credentials',
                groupId: 'com.example.maven-project',
                nexusUrl: 'localhost:8081', 
                nexusVersion: 'nexus3',
                protocol: 'http', 
                repository: 'maven-repo',
                version: '1.0-SNAPSHOT'
              
                    }
                }
           stage ('deploy war/jar tomcat server'){
                steps{                 
                   sh "curl -v -u admin:sunil12345 -T http://localhost:8081/repository/maven-repo/com/example/maven-project/maven-project/1.0-SNAPSHOT/maven-project-1.0-20220914.035934-5.war 'http://localhost:8089\manager\html\upload?path=C:\Program Files\Apache Software Foundation\Tomcat 8.5\webapps'"
             }  
           }
        }
      }
    
