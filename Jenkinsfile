pipeline {
    agent any
    parameters {
        string(name: 'NAME', defaultValue: '', description: 'Who should I say hello to?')
        text(name: 'CUSTOM', defaultValue: '', description: 'Enter some information about the sandwich')
        booleanParam(name: 'TOASTED', defaultValue: true, description: 'Toasted sandwich')
        choice(name: 'CHOICE', choices: ['Cheese toastie', 'Roasted vegie toastie', 'Avocado and fetta toastie'], description: 'Pick something')
        password(name: 'SECRET', defaultValue: '', description: 'Enter a secret')
    }
    stages {
        stage('Test') {
            steps {
                sh 'echo "Build"'
                echo "Name: ${params.NAME}"

            }
        }
        stage('Build artifact') {
            steps {
                sh 'echo "Test"'
                echo "Custom: ${params.CUSTOM}"
            }
        }
        stage('Upload artifact') {
            steps {
                sh 'echo "Deploy"'
                echo "Toasted: ${params.TOASTED}"
            }
        }
        stage('Deploy NonProd') {
            input {
                message 'Proceed?'
                ok 'yes'
                submitter '"${BUILD_USER}"'
            }
            steps {
                sh 'echo "Deploy NonProd"'
                echo "Choice: ${params.CHOICE}"
            }
        }
        stage('SmokeTests NonProd') {
            steps {
                sh 'echo "Deploy NonProd"'
                echo "Choice: ${params.CHOICE}"
                sh 'export DEPLOY_TO_PROD=True'
            }
        }
        stage('Deploy Prod') {
            when {
                allOf {
                    branch 'master'
                    environment name: 'DEPLOY_TO_PROD', value: 'True'
                }
            }
            input {
                message 'Proceed?'
                ok 'yes'
                submitter '"${BUILD_USER}"'
            }
            steps {
                sh 'echo "Deploy Prod"'
                echo "Secret: ${params.SECRET}"
            }
        }
    }
}
