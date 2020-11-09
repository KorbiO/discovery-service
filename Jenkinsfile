pipeline {
	agent any
	tools {
    maven 'maven-3'
    jdk 'java'
  }
  
	stages {
		stage('SCM Checkout'){
			steps{
        	git credentialsId: 'gitPwd', url: 'https://github.com/KorbiO/imdp-latest'
        		}
    }
		stage('Compile') {
			steps {
			withMaven(maven : 'maven-3'){
			
				bat 'mvn -Dmaven.test.failure.ignoire=true clean package'
				
			}	
				  }
		}
		stage('Build Docker Image'){
			steps{
        		bat 'docker build -t omarkorbi/imdb:latest .'
        		}
    }
     stage('Push Docker Image'){
     	steps{
	        bat 'docker login -u omarkorbi -p gotktpas123'
	  		bat 'docker tag imdp:latest omarkorbi/imdp '
	  		bat 'docker push omarkorbi/imdp'
	  		}
    }
    stage('Run Container on Dev Server'){
    	steps{
   	   		bat 'docker run -p 8761:8761 -d --name imdp omarkorbi/imdp:latest'
   	   		}
    }
		
	}
}