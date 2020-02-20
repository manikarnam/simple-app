pipeline {
    agent any
    //tools {
     //   maven 'maven3'
   // }
      
    def sonarUrl = 'sonar.host.url=http://172.17.1.86:9000'
    def mvn = tool (name: 'maven3', type: 'maven') + '/bin/mvn'
    stage('SCM Checkout'){
   
	  git branch: 'master', 
	  credentialsId: 'github', 
	  url: 'https://github.com/javahometech/myweb'
    stages{
        stage('Sonar Publish'){
	   withCredentials([string(credentialsId: 'sonar', variable: 'sonartoken')]) {
        def sonarToken = "sonar.login=${sonartoken}"
        sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	        }
      
        }
        
       stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [
                     [
                         artifactId: 'simple-app', 
                         classifier: '', 
                         file: 'target/simple-app-1.0.0.war', 
                         type: 'war'
                    ]
                ], 
                credentialsId: 'nexus3', 
                groupId: 'in.javahome', 
                nexusUrl: '172.31.15.204:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'simpleapp-release', 
                version: '1.0.0'
            }
        }
    }
}
