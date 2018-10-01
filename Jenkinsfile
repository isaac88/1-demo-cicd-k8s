pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Build Step'
		echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}" 
            }
        }
        stage('Test') {
            steps {
                echo 'Test Step'
            }
        }
        stage('Sonar') {
            steps {
                echo 'Sonar Step'
            }
        }
        stage('Versionate') {
            steps {
                echo 'Versionate Step'
            }
        }
        stage('Bake') {
            steps {
                echo 'Bake Step'
            }
        }
        stage('Contract') {
            steps {
                echo 'Contract Step'
            }
        }
        stage('Store') {
            steps {
                echo 'Store Step'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy Step'
            }
        }
    }
}
