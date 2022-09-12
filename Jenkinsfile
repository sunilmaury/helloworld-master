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
                        file: 'target/webapp.war',
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
            }
        }
    

