pipeline {
	agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		path = "dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
	  	stage('Build') {
			steps{	
				sh 'mvn --version'
				#sh 'docker version'		
		  		echo "Build"
				echo "PATH - $PATH"
				echo "JOB_NAME - $env.JOB_NAME"
	    	}
	  	}
	  	stage('Test') {
			steps{			
		    	echo "Test"
	    	}
	  	}
	  	stage('Integration Test') {
			steps{			
		  		echo "Integration Test"
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