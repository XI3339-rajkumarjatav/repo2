pipeline 
{
  agent any
  environment
  {
      workerType = 'MICRO'
      cloudhub = credentials('cloudhub_credentialrak_4891')
      region= 'us-east-2'
      NEXUS_VERSION = "nexus3"
      NEXUS_PROTOCOL = "http"
      NEXUS_URL = "127.0.0.1:8081"
      NEXUS_REPOSITORY = "maven-nexus-repo"
      NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
  }
  stages 
  {
    stage('Build') 
    {
      steps 
      {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }
    stage('Unit Test') 
    { 
      steps 
      {
        bat 'mvn clean test'
      }
    }
    stage('Deploy Sandbox') 
    { 
      steps 
      {
        bat 'mvn clean deploy -DmuleDeploy -Dmule.version=4.4.0 -Danypoint.username=rak_4891 -Danypoint.password=4891@Rajk -Danypoint.app=payload-transfer -Danypoint.environment=Sandbox'
      }
    }
  }
}
