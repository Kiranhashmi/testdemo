flag=true

pipeline {
    agent any
	parameters {
		//these are types of parameters
		string(name: 'VERSION',defaultValue:'',description:'version to deploy on prod')
		choice (name: 'VERSION',choices:['1.1.0','1.2.0','1.3.0'],description:'')
		booleanParam(name:'executeTests',defaultValue: true, description:'')
	}
    environment {
	//variables defined here can be used by any stage
	NEW_VERSION = '1.3.0'

	    
    }
    stages {
        stage('build') {
            steps {
                echo 'Building Project'
		//using environment variable
		//To output the value of variable in string use " "
		echo "Building version ${NEW_VERSION}"
		
		echo 'successfully installed npm'
            }
        }

	 stage('test') {
		when {
			expression {
				params.executeTests
			} 
		  }    
            steps {
		  
                echo 'Testing Project'
            }
        }
	stage('deploy') {
            steps {
                echo 'Deploying Project'
		echo "DEploying version ${params.VERSION}"
            }
        }	    
   
    }
	post {
	// the conditions here will execute after the build is done
	
	always {
		   //this action will happen always regardless of the result of build   
		   echo 'Post build condition running'
		}
	failure {
		 //this action will happen only if the build has failed 
		  echo 'Post Action if Build Failed'
			
		}	
	}
}
