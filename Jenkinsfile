pipeline{
    
    agent any 
    
    

    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', credentialsId: 'MyJenkins', url: 'https://github.com/jeethu37/demo-counter-app.git'
                }
            }
        }
		
		


		stage('UNIT testing'){

            steps{

                script{

                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){

            steps{

                script{

                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
		
		stage('Maven Building'){

            steps{

                script{

                    sh 'mvn clean install'
                }
            }
        }
		
		stage('Static Code Analysis'){
		
		   steps{
		   
		        script{
				
				   
				   withSonarQubeEnv(credentialsId:'sonar-api') {
				   
				   sh 'mvn clean package sonar:sonar'
				   }
				   
				   }
				   }
				   }
				   
       stage('Quality Gate Status'){
        
         steps{

           script{

                  waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api' 
             }
}
}		

       stage('Upload war file to nexus'){

         steps{

                script{
				
				      def readPomVersion = readMavenPom file: 'pom.xml' 
					  
					  def nexusRepo = readPomVersion.version.endsWith("SNAPSHOT") ? "demoapp-snapshot" : "demoapp-release"


                     nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '54.70.204.243:8081', nexusVersion: 'nexus3', protocol: 'http', repository: nexusRepo, version: "${readPomVersion.version}"
                    

}
}
}

stage('Docker Image Build'){

    steps{

        script{

            sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
            sh 'docker image tag $JOB_NAME:v1.$BUILD_ID jeethu37/$JOB_NAME:v1.$BUILD_ID'
            sh 'docker image tag $JOB_NAME:v1.$BUILD_ID jeethu37/$JOB_NAME:latest'


        }
    }
}



stage('Push image to the docker hub'){

steps{

    script{
             

            withCredentials([string(credentialsId: 'mydocker', variable: 'docker_hub_cred')]) {
    

            sh 'docker login -u jeethu37 -p ${docker_hub_cred}'
            sh 'docker image push jeethu37/$JOB_NAME:v1.$BUILD_ID'
            sh 'docker image push jeethu37/$JOB_NAME:latest'



}

    }
}
			   
}		
             
}

}
