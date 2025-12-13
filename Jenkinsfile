pipeline {
    agent any

    stages {
        stage('Code Clone') {
            steps {
                git url: "https://github.com/Rushitole/two-tier-flask-app.git" , branch: "master"
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
                withCredentials([usernamePassword(
                    credentialsId:"DockerhubCreds",
                    passwordVariable:"dockerHubPass",
                    usernameVariable:"dockerHubUser"
                )]){
                sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                sh "docker tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app:latest"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }

        stage('Deploy') {
            steps {
                sh "docker compose pull && docker compose up -d --build flask-app"
   }
}
}
}
