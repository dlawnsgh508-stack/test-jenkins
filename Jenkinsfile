pipeline {
    // 특정 빌드 노드 지정 시 agent { label 'jenkins-node' } 로 변경 권장
    agent { label "jenkins-node" }
    
    triggers {
        pollSCM('* * * * *')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dlawnsgh508-stack/source-maven-java-spring-hello-webapp.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.153.102:8080')],
                       contextPath: 'hello-world',
                       war: 'target/hello-world.war'
            }
        }
    }
}
