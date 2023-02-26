def gv
pipeline {
    agent any
    environment {
        PIPELINE_VERSION = '1.5'
    }
    parameters {
        choice(name: 'VERSION',choices: ['1.0','1.1','1.2','1.3'], description: '')
        booleanParam(name: 'executeTests' , defaultValue: true, description: '')        
    }
    stages {
        stage('init') {
            steps {
                script{
                    gv = load "script.groovy"
                }
            }
        }
        stage('Build') {
            steps {
                script{
                    gv.buildApp()
                }
            }
        }
      stage('Test') {
            input{
                message "Select the test type"
                ok "Done"
                choice(name: 'ENV',choices: ['A','B','C'], description: '')
            }
            steps {
                script{
                    echo "Testing with ${ENV}"
                    gv.testApp()
                }
            }
        }
      stage('Deploying') {
          when{
                expression {
                    params.VERSION == '1.1'   
                    }
                }
            steps {
                script{
                    env.VAR = input message: "select the environment to deploy to", ok: "Done", parameters: [choice(name: 'ONE',choices: ['dev','staging','prod'], description: '')]    
                }
                
                echo "Deploying the app to ${env.VAR} with pipleline setting version ${env.PIPELINE_VERSION}"
                
            }
        }
    }
}
