pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/AbhaySharma109/php-project.git', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t abhay123321/akshatnewimg6july:v2 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push abhay123321/akshatnewimg6july:v2'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 abhay123321/akshatnewimg6july:v2'
                    sshagent(['sshkeypair']) {
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.39.131 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.39.131 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
