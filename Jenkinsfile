pipeline{
    agent{
        kubernetes {
        }
    }
    stages{
        stage("Clone"){
            steps{
                git branch: 'develop',
                    url: 'https://github.com/ever-co/gauzy.git'
            }
            post{
                always{
                    echo "Cloning repository..."
                }
                success{
                    echo "Cloning successful..."
                }
                failure{
                    echo "Cloning failed! See log for details. Terminating..."
                }
            }
        }
        stage("Docker Image"){
            steps{
                sh 'docker build -t gauzy-api -f .deploy/api/Dockerfile .'
            }
            post{
                always{
                    echo "Starting the Docker Image build..."
                }
                success{
                    echo "Built!"
                }
                failure{
                    echo "====++++A execution failed++++===="
                }
        
            }
        }
        stage("Cleanup Image"){
            steps {
                sh 'docker rmi gauzy-api'
            }
            post{
                always{
                    echo "Cleaning up image cache..."
                }
                success{
                    echo "Cleanup successful..."
                }
                failure{
                    echo "Cleanup failed! See log for details."
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}