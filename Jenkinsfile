pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\jenkins_site\\'
    }

    stages {

        stage('Checkout') {
            steps {
                echo '--- Stage 1: Checkout ---'
                git branch: 'main', url: 'https://github.com/susmitapatil11/Exp6_devops.git'
                echo 'Repository checked out successfully.'
            }
        }

        stage('Validate') {
            steps {
                echo '--- Stage 2: Validate ---'
                bat '''
                    IF NOT EXIST trial.txt (
                        echo ERROR: trial.txt not found!
                        exit /b 1
                    ) ELSE (
                        echo trial.txt found.
                    )

                    IF NOT EXIST Jenkinsfile (
                        echo ERROR: Jenkinsfile not found!
                        exit /b 1
                    ) ELSE (
                        echo Jenkinsfile found.
                    )

                    echo Validation passed successfully.
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo '--- Stage 3: Deploy ---'
                bat '''
                    IF NOT EXIST C:\\jenkins_site (
                        mkdir C:\\jenkins_site
                        echo Created deployment directory C:\\jenkins_site
                    )
                    xcopy /E /I /Y "%WORKSPACE%\\*" "C:\\jenkins_site\\"
                    echo Deployment to C:\\jenkins_site completed successfully.
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully! Site deployed to C:\\jenkins_site\\'
        }
        failure {
            echo 'Pipeline FAILED. Please check the logs above.'
        }
    }
}