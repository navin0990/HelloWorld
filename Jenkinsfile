pipeline {
  agent any
  stages {
    stage('Build Application') { 
      steps {
        bat 'mvn clean install'
      }
    }
 	stage('Test') { 
      steps {
        echo 'Test Appplication...' 
        bat 'mvn test'
      }
    }
 	
   
	stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
            
      steps {
        echo 'Deploying only because of code commit...'
        echo 'Deploying to  dev environent....'
        bat 'mvn package deploy -DmuleDeploy -Dmule.version=4.3.0 -Danypoint.username=navin0990 -Danypoint.password=Navin@0990 -Denv=Sandbox -Dappname=helloworldpipeline -Dbusiness=CTS -DvCore=Micro -Dworkers=1'
      }
	  
	  
	}
  }
}
