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
				
				   withSonarQubeEnv(credentialsId: 'sonar-api') 
				   
				   sh 'mvn clean package sonar:sonar'
				   
				   }
				   }
				   }
				   
		
              
}
}
