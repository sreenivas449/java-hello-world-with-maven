pipeline{
    agent any

    tools {
         maven 'maven'
         jdk 'java'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
            }
        }
        stage('build'){
            steps{
               bat 'mvn package'
            }
        }
        stage('copying the artifact'){
            steps{
                stash includes: 'jb-hello-world-maven-0.2.0.jar', name: 'stash-jar'
            }
        }
        stage('stop service'){
            steps{
                bat 'net stop tomcat-dev'
            }
        }

        stage('unstash artifact'){
            steps{
                dir('C:\\tomcats\\DEV\\apache-tomcat-8.5.76\\webapps') {
                unstash 'stash-jar'
            }

            }
        }
        stage('start service'){
            steps{
                bat 'net start tomcat-dev'
            }
        }

    }
}
