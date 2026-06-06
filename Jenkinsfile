pipeline {
    agent any
    stages {

        stage("git_checkout") {
            steps {
                echo "cloning repository"
                git branch: 'master',
                    url: 'https://github.com/Charan-bavaji/onlinebookstore.git'
                echo "repo cloned successfully"
            }
        }
        stage("build"){
            steps{
                echo"building project...."
                sh'mvn clean package -DskipTests'
                echo "build successful!"
            }
            
        }
        stage("deploy"){
            steps{
                echo "deploying to tomcat..."
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-creds',
                        path '',
                        url: 'http://13.239.199.85:8090'
                    )
                ],
                    contextPath: '',
                    war: 'target/*.war'
                echo "deployed successfully"
            }
        }

    }
}
