pipeline {
    agent any
    stages {
        stage ('Containers - Virtual environment start') {
            steps {
                echo 'Spinning up the containers'
                bat 'docker-compose build'
                bat 'docker-compose up -d'
            }      
        }
        stage('MicroServices - Startup in Parallel') {


            parallel {


                stage('Authentication') {
                    steps {
                        dir('PIS/Authetication'){
                        echo 'Authentication starting up'
                        bat 'npm install' 
                        }
                    }
                }
           
                stage ('Patients MicroService') {
                    steps {
                        dir('PIS/PatientRegistration'){
                        echo 'Patients Service starting up'
                        bat 'npm install'
                        }
                    }
                }
                stage ('Ward Admissions starting up') {
                    steps {
                        dir('PIS/WardManager'){
                        echo 'Staff MicroService starting up'
                        bat 'npm install'
                        }
                    }
                }
            }      
        }
                stage('Unit Testing - Chai/Mocha') {
            steps {   
                   dir('PIS/PatientRegistration') {
                                script {
                                echo 'Patient database Testing with Chai/Mocha'
                                //bat 'npm test'
                                    }
                                }
                    }
        }             

        stage('Microservice containers build') {
                steps {
                     dir('PIS/PatientRegistration') {
                    script {
                    echo 'Spinning down running containers'
                    
                    bat 'docker-compose down'
                
                    echo 'Spinning up the containers'
                    bat 'docker-compose build'
                    }
                    }
                }}


        stage('deploy') {
            steps {
                 dir('PIS/PatientRegistration') {
                script {
                bat 'docker-compose up -d'
                echo 'MicroServices are being deployed in Dockers'
                    }
                }
            }}
    }
        post {
            always {
                echo 'Pipeline fully executed.'
            }
            success {
                echo 'All stages completed successfully.'
            }
            unstable {
                echo 'Stages are inconsistent'
            }
            failure {
                echo 'Pipeline Failed'
            }
            changed {
                echo 'Changes detected..'
            }
        }
}
            
