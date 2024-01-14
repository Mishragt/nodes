pipeline {
    agent any
    stages {
        stage("code pull"){
            steps{
                git url: "https://github.com/Mishragt/nodes.git" , branch: "master"
                echo "code pull hogya"
            }
        }
        stage("code build"){
            steps{
                sh "docker build -t web ."
                echo "file build ho gai"
            }
        }
        stage ("push thee image"){
            steps{
                withCredentials([usernamePassword(credentialsId:"docker",passwordVariable:"pass",usernameVariable:"user")]){
                sh "docker login -u ${env.user} -p ${env.pass}"
                sh "docker tag web ${env.user}/web"
                sh "docker push ${env.user}/web"
                echo "image push ho gya"
                }
            }
        }
        stage ("deploy your app"){
            steps{
                sh "docker-compose down"
                sh "docker-compose up -d"
                echo "deployment done"
            }
        }
    }
}
