pipeline {
    agent any   

    stages {
        stage ('Compile Stage') {
            
            steps {
                mail to:"ruban.yuvaraj@gmail.com", subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p><p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>"
                   
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }

        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
                //notifySuccessful()
            }
        }
    }       
        post {
        success {
            mail to:"ruban.yuvaraj@gmail.com", subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p><p>Check console output for more info.</p>"
        }
        failure {
            mail to:"ruban.yuvaraj@gmail.com", subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p><p>Check console output for more info.</p>"
        }
        unstable {
            mail to:"ruban.yuvaraj@gmail.com", subject:"UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'" body: "<p>UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p><p>Check console output for more info.</p>"
        }     
        changed {
            mail to:"ruban.yuvaraj@gmail.com", subject:"CHANGED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "<p>CHANGED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p><p>Check console output for more info.</p>"
        }
    }
}
