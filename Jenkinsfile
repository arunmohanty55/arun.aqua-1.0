pipeline{
    agent any
    stages{
        stage ('code clon'){
            steps{
                git url: "https://github.com/arunmohanty55/arun.aqua-1.0", branch: 'master'
            }
        }
        stage ('build'){
            steps{
                sh 'docker build -t arun-aqua:1.0 .'
            }
        }
        stage ('test'){
            steps{
               sh 'echo "testing the code"'
            }
        }
        stage ('push to dockerhub'){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockercred",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                    )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag arun-aqua:1.0 ${env.dockerHubUser}/arun-aqua1.0:latest"
                sh "docker push ${env.dockerHubUser}/arun-aqua1.0:latest"
            }
        }
}
        
        stage ('deploy'){
            steps{
               sh '''
            docker rm -f arun-aqua 2>/dev/null || true
            docker run -d --name arun-aqua -p 5000:5000 arun-aqua:1.0
        '''
            }
        }
    }
}
