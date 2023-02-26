def gv
pipeline {
    agent any
    environment {
        PIPELINE_VERSION = '1.5'
    }
    parameters {
        choice(name: 'VERSION',choices: ['1.0',1.1','1.2','1.3'], description: '')
        booleanParam(name: 'executeTests' , defaultValue: true, description: '')        
    }
    stages {
        stage('init') {
            steps {
                script{
                    gv = load"script.groovy"
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
            steps {
                gv.testApp()
            }
        }
      stage('Deploying') {
          when{
                expression {
                    VERSION == '1.1'   
                    }
                }
            steps {
                
                echo 'Deploying the app... $(env.PIPELINE_VERSION)'
            }
        }
    }
}
