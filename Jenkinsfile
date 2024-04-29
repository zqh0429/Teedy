pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test --fail-never'
            }
        }
        stage('doc') {
            steps {
                sh 'mvn javadoc:javadoc --fail-never'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/**/*.xml'
            archiveArtifacts artifacts: 'target/site/apidocs/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
