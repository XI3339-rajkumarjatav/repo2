pipeline {

  agent any

  stages {
    stage('Build') {
      steps {
      		git 'https://github.com/XI3339-rajkumarjatav/repo2.git'
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          bat "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'common-notification-s'
      }
      steps {
      		git 'https://github.com/XI3339-rajkumarjatav/repo2.git'
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="xebia_123" -Danypoint.password="4891@Rajk" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    }

    }
  }

  tools {
    maven 'M3'
  }
}
