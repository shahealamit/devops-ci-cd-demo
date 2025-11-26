pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shahealamit/devops-ci-cd-demo'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo "Stopping Tomcat..."
                sh 'sudo systemctl stop tomcat || true'

                echo "Copying WAR to Tomcat..."
                sh 'sudo cp target/devops-web.war /opt/tomcat/tomcat/webapps/devops-web.war'

                echo "Starting Tomcat..."
                sh 'sudo systemctl start tomcat'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!!"
        }
    }
}
