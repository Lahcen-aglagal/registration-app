 pipline {
   agent { label 'Jenkins-Agent' }
   tools {
     jdk 'Java17'
     maven 'Maven3'
   }
   stages {
     stage ("Cleanup Workspace"){
       steps {
         cleasWs()
       }
     }
     stage("Checkout from SCM"){
       steps{
         git branch: 'main' , credentialsId: 'github' , url : 'https://github.com/Lahcen-aglagal/registration-app.git'
       }
     }
     stage("Build Applicaiton"){
       steps{
         sh "mvn clean package"
       }
     }

     stage("test Application"){
       steps {
         sh "mvn test"
       }
     }

     
   }
 }
