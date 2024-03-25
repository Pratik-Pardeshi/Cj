pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven'
        PATH = "$MAVEN_HOME/bin:$PATH"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Pratik-PardeshiCj.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    def tomcatHome = '/path/to/tomcat'
                    def warFile = sh(returnStdout: true, script: 'find target -name "*.war"').trim()
                    sh "cp $warFile $tomcatHome/webapps/"
                    sh "$tomcatHome/bin/shutdown.sh"
                    sh "$tomcatHome/bin/startup.sh"
                }
            }
        }
    }
    
    post {
        success {
            echo 'Java web application deployed successfully!'
        }
        failure {
            echo 'Java web application deployment failed!'
        }
    }
}
