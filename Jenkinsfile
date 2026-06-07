pipeline {
    agent any

    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build')
        choice(name: 'DEPLOY_ENV', choices: ['dev', 'staging', 'prod'], description: 'Target environment')
    }

    environment {
        TOMCAT_URL = 'http://localhost:8090'
        APP_NAME   = 'onlinebookstore'
        WAR_FILE   = 'target/*.war'
    }

    stages {
        stage("git_checkout") {
            steps {
                echo "cloning repository from branch: ${params.BRANCH}"
                git branch: "${params.BRANCH}",
                    url: 'https://github.com/Charan-bavaji/onlinebookstore.git'
                echo "repo cloned successfully"
            }
        }

        stage("build") {
            steps {
                echo "building ${env.APP_NAME}..."
                sh 'mvn clean package -DskipTests'
                echo "build successful!"
            }
        }

        stage("deploy") {
            steps {
                echo "deploying ${env.APP_NAME} to ${env.TOMCAT_URL} (env: ${params.DEPLOY_ENV})"
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-creds',
                        path: '',
                        url: "${env.TOMCAT_URL}"
                    )
                ],
                contextPath: "${env.APP_NAME}",
                war: "${env.WAR_FILE}"
                echo "deployed successfully!"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline SUCCESS - ${env.APP_NAME} deployed to ${params.DEPLOY_ENV}"
        }
        failure {
            echo "❌ Pipeline FAILED - check logs above"
        }
        always {
            echo "Pipeline completed. Branch: ${params.BRANCH} | Env: ${params.DEPLOY_ENV}"
        }
    }
}
