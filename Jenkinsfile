pipeline {
	agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		path = "dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
	  	stage('Checkout') {
			steps{	
				sh 'mvn --version'						
		  		echo "Build"
				echo "PATH - $PATH"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_NUMBER - $env.NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
	    	}
	  	}
	  	stage('Compile') {
			steps{			
		    	sh "mvn clean compile"
	    	}
	  	}
		stage('Test') {
			steps{			
		    	sh "mvn test"
	    	}
	  	}
	  	stage('Package') {
			steps{			
		  		sh "mvn package -DskipTests"
	   		}
	  	}

		stage('Integration Test') {
			steps{			
		  		sh "mvn failsafe:integration-test failsafe:verify"
	   		}
	  	}

		stage('Build Docker Image') {
			steps{			
		  		script{
					dockerImage = docker.build("gopinathc/hello-world-java:$env.BUILD_TAG")
				}
	   		}
	  	}
		stage('Push Docker Image') {
			steps{			
		  		script{
					docker.withRegistry('', 'dockerhub'){
					dockerImage.push();
					dockerImage.push(latest);
					}
				}
	   		}
		}
	} 
	post{
		always{
			echo "Execute Always"
		}
		success{
			echo "Executed Sucessfully"
		}
		failure{
			echo "Script Failed"
		}
		changed{
			echo "Status of build changed"
		}
	}
}