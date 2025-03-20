pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("Test") {
            steps {
                sh "mvn test"
            }
        }
        stage("Build") {
            steps {
                sh "mvn package"
            }
        }
        stage("Deploy on Test") {
            steps {
                // List the contents of the target directory for debugging
                sh "ls -l target/"
                
                // Deploy to Tomcat
                script {
                    try {
                        deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', url: 'http://54.204.71.212:8080/manager/text')], contextPath: '/app', war: 'target/*.war'
                    } catch (Exception e) {
                        echo "Deployment failed: ${e}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }
    }
}
