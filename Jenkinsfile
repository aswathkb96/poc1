pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/ravdy/javaloginapp.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
       }
       
       stage('SonarQube analysis') {
        steps{
        withSonarQubeEnv('sonarqube-8.9') { 

        sh "mvn sonar:sonar"
        }
        }
        }
       stage('Junit'){
            steps{
                sh 'mvn test'
            }
       }
       stage('Jacoco'){
            steps{
                sh 'mvn jacoco:report'
            }
       }
       stage('Nexus'){
            steps{
                sh 'mvn deploy'
            }
       }
        //stage('Deploy To Tomcat'){
        //sshagent(['app-server']) {
         //   sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@ec2-54-165-137-181.compute-1.amazonaws.com:/opt/apache-tomcat-9.0.78/webapps'
       // }
   // }
       stage('Mail'){
            steps{
 		mail bcc: '', body: 'Done', cc: '', from: '', replyTo: '', subject: 'Build Report', to: 'aswatha619@gmail.com'
            }
       }
       
    }
}
