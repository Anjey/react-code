pipeline{
    agent any
    
    stages{
    
        stages{
        stage('Checkout') {
            steps {
                deleteDir()
                checkout scm
            }
        }
    
        // stage ('Prepare source and init vars'){
        //     agent any
        //     steps {
        //     echo 'git pull'
        //     git branch: '$branch', credentialsId: 'github-react', url: 'https://github.com/Anjey/react-code.git'
        //         script {
        //             sh 'git submodule update --recursive --init --remote'
        //             sh 'git --git-dir="./.git" --work-tree="./" describe --always > ./VERSION.txt'
                    
        //         }
        //     }
        // }
        
         stage ('yarn install'){
            agent any
            steps {
                 sh '''
                    yarn install
                    '''
                }
            }
            
        stage ('yarn build'){
            agent any
            steps {
                 sh '''
                    yarn build
                    '''
                }
            }
            
        stage('build infra'){
            steps{
                script{
                   if (branch == 'main') {
              build job: "react-project-infra", parameters: [
                string(name: 'BRANCH_PROD' , value: "${branch}")
            ],
            wait:false
            }
            else {
              build job: "react-project-infra", parameters: [
                string(name: 'BRANCH_DEV' , value: "dev")
            ],
            wait:false
            }
            }
                }
            
            }
        }
        
         
}