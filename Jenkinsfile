pipeline {
    agent any

    environment {
        function_name = 'prag-lambda'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the test'
                sh 'mvn package'
            }
        }

        stage('Push') {
            steps {
                echo 'Pushing'

                sh "aws s3 cp target/sample-1.0.3.jar s3://prag-s3"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Build'

                sh "aws lambda update-function-code --function-name $function_name --region us-east-1 --s3-bucket prag-s3 --s3-key sample-1.0.3.jar"
            }
        }
    }
}
