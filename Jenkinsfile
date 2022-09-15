pipeline {
	agent { docker {image 'maven:3.8.6'} }
	stages{
	  	stage('Build') {
			steps{	
				sh 'mvn --version'		
		  		echo "Build"
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