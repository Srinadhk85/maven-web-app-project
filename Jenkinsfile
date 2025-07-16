pipeline {
    agent any
    tools
    {
        maven "maven-3.9.9"
    }
    stages {
         stage('checkout stage') { 
            steps {
           git branch: 'development', url: 'https://github.com/Srinadhk85/maven-web-app-project.git'
            }
        }
        stage ('Build'){
            steps{
                sh "mvn clean package"
            }
        }
          stage('SonarQube Analysis') {
      steps {
         sh 'mvn sonar:sonar'
            }
          }
            stage('Deploy to Nexus') {
      steps {
         sh 'mvn deploy'
            }
          }
stage('DeployAppToTomcat'){
   steps{
        sh """
            curl -u kk:password \
            --upload-file /var/lib/jenkins/workspace/Declarative-PL-jio/target/maven-web-application.war \
            "http://54.166.109.79:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """

          }
        }
}
}
