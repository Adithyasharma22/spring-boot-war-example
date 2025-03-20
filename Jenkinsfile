pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test fdfd
                sh "mvn test"
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugi
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', url: 'http://54.204.71.212:8080/manager/text')], contextPath: '/app', war: 'target/*.war'
              
            }
            
        }
    }
}
