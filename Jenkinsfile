pipeline {
    agent any

    environment {
        function_name = 'lambda'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'mvn package'
            }
        }

        stage('Push') {
            steps {
                echo 'Push'

                sh "aws s3 cp target/sample-1.0.3.jar s3://jenkinsbuckets1"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Build'

                sh "aws lambda update-function-code --function-name $function_name --region us-west-1 --s3-bucket jenkinsbuckets1 --s3-key sample-1.0.3.jar"
            }
        }
    }
}
