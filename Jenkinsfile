pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('anypoint.credentials')
    MULE_VERSION = '4.3.0'
    BG = "CTS"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
		  echo 'Test Appplication...'
          bat "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'HelloWorldPipeline'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -DapplicationName="%APP_NAME%" -Denvironment="%ENVIRONMENT%" -Dbg="%BG%" -Dworker="%WORKER%"'
      }    }
    stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Design'
        APP_NAME = 'HelloWorldPipeline'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -DapplicationName="%APP_NAME%" -Denvironment="%ENVIRONMENT%" -Dbg="%BG%" -Dworker="%WORKER%"'
      }
    }
  }

  tools {
    maven 'M3'
  }
}