pipeline{
    agent any
    
    environment{
        DIRECTORY_PATH = "/project_directory"
        TESTING_ENVIRONMENT = "test_env"
        PRODUCTION_ENVIRONMENT = "prod_env"
    }
    stages{
        stage('Build'){
            steps{
                echo "fetch the source code from the directory path specified by the environment variable"
                echo "compile the code and generate any necessary artifacts"
            }
        }
            stage('Test'){
                steps{
                    echo"unit tests"
                    echo"integration tests"
                }
            }
            
            stage('Code'){
                steps{
                    echo"check the quality of the code"
                }
            }
            stage('Deploy'){
                steps{
                    echo "deploy the application to a testing environment specified by the environment variable"
                }
            }
            stage('Approval'){
                steps{
                    sleep 10
                    echo "Approved"
                }
            }
            stage(' Deploy to Production'){
                steps{
                    echo "${PRODUCTION_ENVIRONMENT} code deployed to production"
                }
            }
        }
    }
