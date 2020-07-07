pipeline {
    agent any

    //tools {
      //  maven "3.6.0" // You need to add a maven with name "3.6.0" in the Global Tools Configuration page
    //}

    stages {
        stage("Build") {
            steps {
               // sh "mvn -version"
                sh "mvn clean install"
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

//git credentialsId: 'git', url: 'ssh://git@192.168.15.5:30022/root/firstproject.git'