pipeline{
    agent any
    stages{
        stage('Start Grid'){
            steps{
                bat 'docker-compose -f grid.yaml up -d'
            }
        }
        stage('Run Test'){
            steps{
                bat 'docker-compose -f test_suite.yaml up'
            }
        }
    }
    post{
        always{
            sh 'docker-compose -f grid.yaml down'
            sh 'docker-compose -f test_suite.yaml down'
        }
    }
}