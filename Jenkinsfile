pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }
      }
       stage('Unit Test') {
            steps {
              sh "mvn test"
              }
         } 
      stage('Docker build and push') {
            steps {
              withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
                sh "printenv"
                sh 'docker build -t svnemma/numeric-app:""$GIT_COMMIT"" .'
                sh 'docker push svnemma/numeric-app:""$GIT_COMMIT""'
              }
         }   
    }
}
}  
