pipeline {
    agent {
        label 'agent'
    }

    stages {
        stage('check out from SCM') {
            steps {
                git 'https://github.com/saikumarsagar/project1-docker.git'
            }
        }

    stage('MVN Build and Junit testing by MVN') {
            steps {
             sh 'mvn clean package'
           //   junit 'target/surefire-reports/*.xml'
            }
        } 
    stage('Docker build') {
            steps {
               // for 2nd time running job, to avoid conflicts removing previous builds and images
              //  sh 'sudo docker stop javacal'            
               // sh 'sudo docker rm -f javacal'
                sh 'sudo docker rm -f saidocker2048/project:3.0'
              // building docker image
             sh 'sudo docker build -t saidocker2048/project 3.0 .'
            }
        }
        
     stage('Running Docker container') {
            steps {
                
              sh 'sudo docker run -dt -p 8098:8080 --name=javacal2 saidocker2048/project:3.0'
            }
        }  

             stage('testing') {
            steps {
                
              sh echo 'test'
            }
        }   
     stage('Pushing Image to docker hub') {
            steps {
            withCredentials([string(credentialsId: '6636d3c5-1154-4ac0-8d3d-5f5649a671b7', variable: 'docker')])
           // {
           sh "sudo docker login -u saidocker2048 -p ${docker}"
           sh 'sudo docker push saidocker2048/project:4.0'
          //  }

            }
        }  
        
          
    }
}
