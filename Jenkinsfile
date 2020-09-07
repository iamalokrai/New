pipeline {

  agent any
  environment {
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.3.0'
    BG = "Alok"
    WORKER = "MICRO"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean install package'
      }
    }


     stage('Dev Deployment') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'new-app'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    }
  }

 
}