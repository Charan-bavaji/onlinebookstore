pipeline {
    agent any
    environment {
       TOMCAT_URL = 'https://localhost:8080'
       APP_NAME = 'onlinebookstore'
    }
    stages {

        stage("git_checkout") {
            steps {
                echo "cloning repository"
                git branch: 'master',
                    url: 'https://github.com/Charan-bavaji/onlinebookstore.git'
                echo "repo cloned successfully"
            }
        }

        stage("build") {
            steps {
                echo "building project..."
                sh 'mvn clean package -DskipTests'
                echo "build successful!"
            }
        }

        stage("deploy") {
            steps {
                echo "deploying to tomcat..."
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-creds',
                        path: '',
                        url: ${TOMCAT_URL}
                    )
                ],
                contextPath: '',
                war: 'target/*.war'
                echo "deployed successfully!"
            }
        }


    }
        post {
    success {
        echo "✅ Build & Deploy SUCCESS"
    }
    failure {
        echo "❌ Build or Deploy FAILED"
    }
    always {
        echo "Pipeline finished. Cleaning up if needed."
    }
}
}
