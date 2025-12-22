@Library("shared") _
pipeline {
    agent any

    stages {
        stage('Code Clone') {
            steps {
                script{
                    clone("https://github.com/Rushitole/Two-Tier-Flask-App-Rushi.git" ,"master")
                    
                }
            }
        }
        
        stage("Trivy Files System Scan"){
            steps{
                script{
                    trivy_fs()
                }
               
            }
        }

        stage('Build') {
            steps {
                sh "docker build -t two-tier-flask-app . "
            }
        }

        stage('Test') {
            steps {
                echo "Tester/developer ne test cases bhi likh diye"
            }
        }
        
        stage("push to docker hub"){
            steps{
               script{
                   docker_push("DockerhubCreds","two-tier-flask-app")
               }
            }
        }

        stage('Deploy') {
            steps {
                sh "docker compose pull && docker compose up -d --build flask-app"
   }
}
}
post{
    success{
        script{
            mail (
            to: 'prernasable05@gmail.com',
            subject: "Build successed",
            body: 'This app Build successfully using jenkins CI/CD Pipeline '
          )  
        }
    }
    
    
    failure{
        script{
            mail(
            to: 'prernasable05@gmail.com',
            subject: "Build successed",
            body: 'This app failed to Build using jenkins CI/CD Pipeline '
          ) 
        }
    }
    
}
}
