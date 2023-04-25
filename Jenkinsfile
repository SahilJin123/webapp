pipeline {
    agent {
        label 'Slave1'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
         stage('Sonar-Report') {
             steps {
             sh 'mvn clean install sonar:sonar \
  -Dsonar.projectKey=Jenkins_Project \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=d87d28cce268734b4a4fa21ffd0348ffe72f4605'
             }
         }
        stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
         stage('Nexus-deploy') {
             steps {
                 bat 'mvn clean deploy'
             }
         }
    }
}
