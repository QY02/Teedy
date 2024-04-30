pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('doc') {
            steps {
                sh 'mvn javadoc:javadoc --fail-never'
                sh 'mvn javadoc:jar --fail-never'
                sh 'mvn javadoc:aggregate --fail-never'
                sh 'mvn javadoc:aggregate-jar --fail-never'
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}