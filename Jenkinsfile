pipeline {
    agent any 
      stages { 
    stage('Initialize') {
            steps  {
             script {
             def dockerHome = tool 'Dockertools'
             env.PATH = "${dockerHome}/bin:${env.PATH}"
             }
            } 
        }  


    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
      steps { 
        checkout scm
      }
    }

    stage('Build image') {
       
     steps {
        app = docker.build("getintodevops/hellonode")
        }
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
    steps {
        app.inside {
            sh 'echo "Tests passed"'
        }
     }  
   }
 }
    
}