pipeline{
    agent any
    tools {
  git 'Default'
  maven 'maven'
}

    stages{
        stage("checkout code"){
            steps{
                echo "========executing checkout code========"
                checkout([$class: 'GitSCM', branches: [[name: '*/sangee']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sange6/simple-java-maven-app.git']]])
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========checkout code executed successfully========"
                }
                failure{
                    echo "========checkout code execution failed========"
                }
            }
        }
        stage("bulid"){
            steps{
                echo "========executing bulid========"
                sh 'mvn clean install'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========bulid executed successfully========"
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                }
                failure{
                    echo "========bulid code execution failed========"
                }
            }
        }
        stage("unit test"){
            steps{
                echo "========executing test========"
                sh 'mvn test'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========test executed successfully========"
                    junit 'target/surefire-reports/*.xml'
                }
                failure{
                    echo "========test code execution failed========"
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage("sonar scan"){
            steps{
                echo "========executing sonar scan========"
                withSonarQubeEnv('mysonarscaner') {
                    sh "${tool('mysonar')}/bin/sonar-scanner \
                        -Dsonar.projectKey=simple-java-maven-app \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target/* \
                        -Dsonar.host.url=http://172.31.7.196:9000 \
                        -Dsonar.login=sqa_10d194b8b80439bd2845bab35ed96d8c144bd4ab"
                }
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========test executed successfully========"
                    
                }
                failure{
                    echo "========test code execution failed========"
                    
                }
            }
        }
         stage("upload to nexus"){
            steps{
                echo "========uploading artifact========"
                sh 'mvn -s settings.xml deploy'
                
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========uploading successfully========"
                    
                }
                failure{
                    echo "========uploading failed========"
                    
                }
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
