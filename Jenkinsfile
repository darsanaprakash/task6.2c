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
            stage('Unit and Integration Test'){
                steps{
                    echo"unit tests"
                    echo"integration tests"
                    
                    emailext (
                subject: "Jenkins Build ${env.build_number} - Test Stage ${currentBuild.result}",
                body: "This is to notify you that the Test stage of build ${env.build_number} has successfully completed with status: SUCCESS.",
                to: 's223161963@deakin.edu.au',
                attachLog: true
                        )
                }
            }
            
            stage('Code Analysis'){
                steps{
                    echo"check the quality of the code"
                    echo "using sonarqube for checking the code quality"
                }
            }
            stage('Security scan'){
                steps{
                    echo "Security scan using OWASP Dependency-Check plugin for checking project dependencies for vulnerabilities"
            
                    emailext (
                subject: "Jenkins Build ${env.build_number} - Security Scan Stage ${currentBuild.result}",
                body: "This is to notify you that the Security Scan stage of build ${env.build_number} has completed with status: SUCCESS.",
                to: 's223161963@deakin.edu.au',
                attachLog: true
                        )
                }
            }
           
            stage(' Deploy'){
                steps{
                     echo "deploy the application to a testing/staging environment in an AWS EC2 instance"
                 echo "test environment: ${test_env}"
                }
            }
        stage(' Integration Tests on staging'){
                steps{
                     echo "Running integration tests on staging environment"
                echo "Tests complete"
                }
            }
         stage('Deploy to production') { //production deployment
             
             steps{
                 echo "Deploying to production environment: ${prod_env}"
                 echo "Deployed to production!"
             }
       
    }                
        }
   post{
        always{
        emailext (
      subject: "SUCCESSFUL: Job '${env.job_name} [${env.build_number}]'",
      body: """<p>SUCCESSFUL: Job '${env.job_name} [${env.build_number}]':</p>
        <p>Check console output at &QUOT;<a href='${env.build_url}'>${env.job_name} [${env.build_number}]</a>&QUOT;</p>""",
      to: "s223161963@deakin.edu.au"
    )                     
                        
    }
   }
 }
