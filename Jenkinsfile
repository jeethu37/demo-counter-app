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

       stage('war file to nexus'){

         steps{

                script{


                     nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '52.33.237.5:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'demoapp-release', version: '1.0.0'
                       
}
}
}
					   
				   
		
              
}
}
