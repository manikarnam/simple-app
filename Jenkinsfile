pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages{
        stage('Build'){
            steps{
                 bat label: '', script: 'mvn clean package'
            }
        }
  
        stage('publish to nexus'){
            steps{
                
            nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'target/simple-app-1.0.0.war', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '172.17.1.86', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://172.17.1.86:8081/repository/maven-releases/', version: '1.0.0'
            
            
            }
            
        }
    }
}
