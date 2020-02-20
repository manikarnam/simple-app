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
   }
}
