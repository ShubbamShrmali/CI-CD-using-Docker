pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/ShubbamShrmali/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t docker-project:latest .' 
                sh 'docker tag samplewebapp shubbamshrmali/docker-project:latest'
                //sh 'docker tag samplewebapp shubbamshrmali/docker-project:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: https://hub.docker.com/repository/docker/shubbamshrmali/docker-project ]) {
          sh  'docker push shubbamshrmali/docker-project:latest'
        //  sh  'docker push shubbamshrmali/docker-project:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 shubbamshrmali/docker-project"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ec2-user@3.84.124.42run -d -p 8003:8080 shubbamshrmali/docker-project"
 
            }
        }
    }
	}
    
