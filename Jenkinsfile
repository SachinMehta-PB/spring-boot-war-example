pipeline{
    agent any
    tools {
        maven 'maven'
    }
    stages{
        stage("HelloWorld-Test"){
            steps{
                //mvn test for testing
                sh "mvn test"
                slackSend channel: 'jenkins-channel', message: 'Job Started'
            }
        }
        stage("HelloWorld-Build"){
            steps{
                //mvn package for building
                sh "mvn package"
            }
        }
        stage("HelloWorld-DeployToTest"){
            steps{
                //Deploy on container -> Plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat9credentials', path: '', url: 'http://18.188.44.73:8080')], contextPath: '/app2', war: '**/*.war'
            }
        }
        stage("HelloWorld-DeployToProduction"){
            input {
                message "Would you like to continue"
                ok "Yes"
            }
            steps{
                //Deploy on container -> Plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat9credentials', path: '', url: 'http://3.22.57.53:8080')], contextPath: '/app2', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend channel: 'jenkins-channel', message: 'Job Success'
        }
        failure{
            echo "========pipeline execution failed========"
            slackSend channel: 'jenkins-channel', message: 'Job Failed'
        }
    }
}
