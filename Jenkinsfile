pipeline {
    agent any
    stages {
        stage('Git-Checkout') {
            steps {
                echo 'Git-Checkout'
                git branch: 'main', credentialsId: '9342c22b-7c07-476c-a84b-e138d5219e1c', url: 'https://github.com/Senthilprabhu1/helloworld-war.git'
            }
        }
		stage('Build') {
            steps {
                echo 'Ant build'
                withAnt(installation: 'ANT', jdk: 'JAVA8') {
                    //for windows 
                    bat "ant"
                }
            }
        }
		stage('Scan') {
            steps {
                echo 'Malware Scan'
            }
        }
		stage('Test') {
            steps {
                echo 'Sonar Test'
            }
        }
		stage('Deploy') {
            steps {
                echo 'Weblogic deploy'
                deploy adapters: [tomcat8(credentialsId: '366db3f9-660a-4ec5-b393-72baf6f0a867', path: '', url: 'http://localhost:8080/')], contextPath: 'antwebapp2', war: '**/*.war'
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
		success { 
            echo 'I will always say success again!'
        }
		failure { 
            echo 'I will always say failure again!'
        }
		unstable { 
            echo 'I will always say unstable again!'
        }
		changed { 
            echo 'I will always say changed again!'
        }
    }
}
