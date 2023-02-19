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
              
}
}
