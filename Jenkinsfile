pipeline{
    agent any
    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
        choice choices: ['1', '2', '3', '4'], description: 'Select the thread count', name: 'THREAD_COUNT'
    }
    stages{
        stage('Start Grid'){
            steps{
                bat "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
            }
        }
        stage('Run Test'){
            steps{
                bat "docker-compose -f testsuite.yaml up"
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f testsuite.yaml down"
            archiveArtifacts artifacts: 'output/test-output/index.html', followSymlinks: false
        }
    }
}