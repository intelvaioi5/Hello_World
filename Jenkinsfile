pipeline{

  agent any
 
  stages{
  
    stage("Git Checkout"){
        steps{
         git 'https://github.com/intelvaioi5/Hello_World.git'
		 }
    }
    
    stage("MVN Packaging"){
       steps{
        def M2_Home = tool name: 'M2_HOME', type: 'maven'
        def mvnCMD = "${M2_Home}/bin/mvn"
        sh "${mvnCMD} clean package"
        sh 'pwd'
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
        def dockerlog ='docker run -p 8080:8080 -d --name tomcat1 dockerfocus/tomcat:1.0.0'
        sshagent(['awslogin']) {
        sh "ssh -o StrictHostkeyChecking=no ec2-user@54.157.164.125 ${dockerlog}"
}
 }
    }
  }
}
