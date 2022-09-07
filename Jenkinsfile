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
                deploy adapters: [tomcat9(credentialsId: 'tomcat9credentials', path: '', url: 'http://18.188.44.73:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
        stage("HelloWorld-DeployToProduction"){
            steps{
                //Deploy on container -> Plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat9credentials', path: '', url: 'http://3.22.57.53:8080')], contextPath: '/app', war: '**/*.war'
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
