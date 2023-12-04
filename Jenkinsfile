pipeline{
 agent any
 
 stages{
     stage("Code Clone"){
      steps{
          echo "doing code"
          git url:"https://github.com/7Aditya5/django-notes-jenkins-declarative.git",branch: "master"
      }   
     }
     stage("Build"){
      steps{
          echo "doing build"
          sh "docker build -t my-notes-app ."
      }     
     }
     stage("Push to docker hub"){
         steps{
          echo "doing push to docker hub" 
          withCredentials([usernamePassword(credentialsId: "dockerhub",passwordVariable: "dockerhubPass", usernameVariable: "dockerhubUser")]){
              sh "docker tag my-notes-app ${env.dockerhubUser}/my-notes-app:latest"
              sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
              sh "docker push ${env.dockerhubUser}/my-notes-app:latest"
          }
      }  
     }
     stage("Deploy"){
         steps{
         echo "doing deployment" 
         sh "docker-compose down && docker-compose up -d"
         
      }  
     }
 }
}
