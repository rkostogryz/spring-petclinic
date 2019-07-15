pipeline {
    agent any
    //tools {
    //   maven "Maven 3.6.1"
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B verify'
            }
        }
        stage('test') {
            steps {
                sh "mvn -B test"
            }
        }
        stage('deploy to nexus') {
            steps {
                nexusArtifactUploader(
                        nexusVersion: 'nexus2',
                        protocol: 'http',
                        nexusUrl: '172.17.0.3:8081/nexus',
                        groupId: 'org.springframework.samples',
                        version: '2.1.0.BUILD-SNAPSHOT',
                        repository: 'jenkins',
                        credentialsId: 'nexus_dp',
                        artifacts: [
                                [artifactId: 'spring-petclinic',
                                 classifier: '',
                                 file      : 'spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar',
                                 type      : 'jar'
                                ]
                        ]
                )
            }
        }
    }
}