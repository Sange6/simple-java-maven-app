pipeline{
    agent any
    stages{
        stage('checkout'){
            steps(
                script{
                    checkout([$class: 'GitSCM', branches: [[name: 'pipeline testing']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sange6/simple-java-maven-app.git']]])

                }
            )

        }
        
    }
}