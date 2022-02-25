pipeline 
{
  agent any
  environment{
      workerType = 'MICRO'
      region= 'us-east-2'
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "127.0.0.1:8081"
        NEXUS_REPOSITORY = "maven-nexus-repo"
        NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
  }
  stages 
  {
   stage('SCM-Checkout') {
     steps {
         git branch: 'patch-3', 
             credentialsId: 'XI3339-rajkumarjatav', 
             url: 'https://github.com/XI3339-rajkumarjatav/repo2.git'
     }
   }
    stage('Build') 
    {
      steps 
      {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }
    stage("Publish to Nexus Repository Manager") {

            steps {

                script {

                    pom = readMavenPom file: "pom.xml";
                    
                    filePath = (pom.name + "-" + pom.version + "-" + pom.packaging + ".jar") ;
                    
                    echo "filepath, ${filePath}" ;
                                     
                    echo "('target/'+${filePath})" ;

                    filesByGlob = findFiles(glob: ("target/"+filePath));
                    
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}" ;

                    artifactPath = filesByGlob[0].path;

                    artifactExists = fileExists artifactPath;
                    
                    echo "artifactPath, ${artifactPath}" ;

                    if(artifactExists) {

                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";

                        nexusArtifactUploader(

                            nexusVersion: NEXUS_VERSION,

                            protocol: NEXUS_PROTOCOL,

                            nexusUrl: NEXUS_URL,

                            groupId: pom.groupId,

                            version: pom.version,

                            repository: NEXUS_REPOSITORY,

                            credentialsId: NEXUS_CREDENTIAL_ID,

                            artifacts: [

                                [artifactId: pom.artifactId,

                                classifier: '',

                                file: artifactPath,

                                type: ('jar') ],

                                [artifactId: pom.artifactId,

                                classifier: '',

                                file: "pom.xml",

                                type: "pom"]

                            ]

                        );

                    } else {

                        error "*** File: ${artifactPath}, could not be found";

                    }

                }

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
