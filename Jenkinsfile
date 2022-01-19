pipeline { 
    agent any  
    tools { 
        maven 'Maven' 
        jdk '1.11' 
    }
    stages { 
	stage('Update Dependencies') {
	    steps {
		sh 'mvn versions:use-latest-verions processParent=true'
            }
    	}
        stage('Compile') { 
            steps { 
               sh 'mvn clean compile'
            }
        }
        stage('Test'){
        	steps {
        		sh 'mvn test'
        	}
        	post {
                always {
	                    junit testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true
                }
            }
        }
	stage('Commit dependency updates') {
		steps {
			sh 'mvn versions:commit'
			sh 'mvn -Dmessage="updateing dependencies" scm:checkin'
		}
	}
    }
}
