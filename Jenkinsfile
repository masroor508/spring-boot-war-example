pipeline{
    agent any
    tools {
        maven 'maven' 
    }
    stages{
        stage("test"){
            steps{
                sh 'mvn --version'
                sh 'mvn test'
                echo "Testing is done"
            }
        }
        stage("build"){
            steps{
                sh 'mvn package'
                echo "Building the app"
            }
        }
        stage("deploy on test"){
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '945e6e91-7a93-449c-88a2-f22547b71e47', path: '', url: 'http://43.204.145.83:8081')], contextPath: '/app', war: '**/*.war'
                echo "Deploying on testing server"
            }
        }
        stage("Deploy on prod"){
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '945e6e91-7a93-449c-88a2-f22547b71e47', path: '', url: 'http://http://52.66.93.83:8080')], contextPath: '/app-prod', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
