pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }
        } 
    
      stage('Unit Tests - JUnit and JaCoCo') {
        steps {
          sh "mvn test"
           }
        }
      stage('Docker Build and Push') {
         steps {
           withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
            sh 'printenv'
            sh 'sudo docker build -t vspvijay/numeric-app:""$GIT_COMMIT"" .'
            sh 'docker push vspvijay/numeric-app:""$GIT_COMMIT""'
           }
        }  
      }

   }
}
