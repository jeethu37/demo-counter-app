pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', credentialsId: 'MyJob', url: 'https://github.com/jeethu37/demo-counter-app.git'
                }
            }
        }
              
}
}
