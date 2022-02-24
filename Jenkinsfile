pipeline 
{
  agent any
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
      environment 
      {
        ANYPOINT_CREDENTIALS = credentials('rak_4891')
      }
      steps 
      {
        bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=4.3.0 -Danypoint.username="rak_4891" -Danypoint.password="4891@Rajk" -Dcloudhub.environment=SANDBOX'  
      }
    }
  }
}
