pipeline {
    environment {
        TOKEN = credentials('SURGE_TOKEN')
      }
    agent {
        docker { 
            image 'josedom24/debian-npm'
            args '-u root:root'
        }
    }
    stages {
        stage('Clone') {
            steps {
                git branch:'master',url:'https://github.com/machde-testing//ic-html5.git'
            }
        }
        
        stage('Install surge') {
            steps {
                sh 'npm install -g surge'
            }
        }
        
        stage('Install Pip') {
            steps {
                sh 'apt update -y && apt install pip default-jre -y'
            }
        }
       
        stage('Install Dependencies') {
            steps {
                sh 'pip install html5validator '
            }
        }
       
        stage('Test HTML') {
            steps {
                sh 'html5validator --root _build/'
            }
        }
        stage('Deploy')
        {
            steps{
                sh 'surge ./_build/ machde-testing.surge.sh --token $TOKEN'
            }
        }
        
    }
}
