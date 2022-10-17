pipeline {
    agent { label 'openjdk' }
        stages { 
        stage('teju') {
            steps {
                git url: "https://github.com/tejugoud11/openmrs-core.git", branch: "${params.CHOICES}"
            
            }
        }
        stage('jenkins'){
            steps{
                sh  "mvn ${params.DEPLOY_ENV}"
            }
        } 
        stage('liljen') {
            steps{
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
            }
        }
        stage('java'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }
    parameters{
        choice(name: 'CHOICES', choices: ['master'], description: 'openmrs')
        string(name: 'DEPLOY_ENV', defaultValue: 'clean', description: 'test')
    }
    post{ 
        always{
            echo "build completed"
        }
        success{
            echo "build success"
        }
        failure{
            echo "build failed"
        }
    }
}