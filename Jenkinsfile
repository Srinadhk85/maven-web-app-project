node {

    // Define Maven tool from Jenkins global configuration
    def mavenHome = tool name: 'maven-3.9.9'

    // Stage 1: Checkout source code from Git
    stage('git checkout')
    {
      git branch: 'development', url: 'https://github.com/Srinadhk85/maven-web-app-project.git' 
    }
    
    // Stage 2: Compile the application
    stage('Compile') {
        sh "${mavenHome}/bin/mvn clean compile"
    }
	
    
    // Stage 2: Build the application and package it (.war/.jar)
    stage('Build') {
        sh "${mavenHome}/bin/mvn clean package"
    }
    // Stage 4: Generate SonarQube report
	stage('SonarQube  Report') {
         sh "${mavenHome}/bin/mvn sonar:sonar"
	}
	// Stage 5: Upload artifact
	stage('Upload to Nexus') {
    sh "${mavenHome}/bin/mvn deploy"
    }
    //Stage 6: Deploy to Tomcat
    stage('Deploy to Tomcat') {
    echo "Deploying WAR file using curl..."

    sh """
        curl -u kk:password \
        --upload-file /var/lib/jenkins/workspace/sciptedPL-ci-cd-job/target/maven-web-application.war \
        "http://52.207.212.160:8080/manager/text/deploy?path=/maven-web-application&update=true"
    """
   }
} 
