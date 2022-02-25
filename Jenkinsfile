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
      steps 
      {
        bat 'mvn clean deploy -DmuleDeploy -Dmule.version=4.4.0 -Danypoint.username=rak_4891 -Danypoint.password=4891@Rajk -Danypoint.app=payload-transfer -Danypoint.environment=Sandbox'
      }
    }
  }
}
