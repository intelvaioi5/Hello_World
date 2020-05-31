pipeline{

  agent any
  tools{
	
	maven 'M2_HOME'
 
 }
	environment{
	dockerlog = "docker run -p 8080:8080 -d --name tomcat1 dockerfocus/tomcat:1.0.0"
	}
  stages{
  
    stage("Git Checkout"){
        steps{
         git 'https://github.com/intelvaioi5/Hello_World.git'
		 }
    }
    
    stage("MVN Packaging"){
       steps{
        sh 'mvn clean package'
	   }
    }
    
    stage("Build Docker Image"){
       steps{ 
        sh 'docker build -t dockerfocus/tomcat:1.0.0 .'
	   }
    }
    stage("Push Image"){
	   steps{
        withCredentials([string(credentialsId: 'dockerPWD', variable: 'dockerpwd')]) {
       sh "docker login -u dockerfocus -p ${dockerpwd}"
}
        sh 'docker push dockerfocus/tomcat:1.0.0'
	   }
    }
    stage("create container"){
	   steps{
        
        sshagent(['awslogin']) {
        sh "ssh -o StrictHostkeyChecking=no ec2-user@3.90.80.85 ${dockerlog}"
}
 }
    }
  }
}
