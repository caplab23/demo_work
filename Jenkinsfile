pipeline {
    agent any

    environment {
        // path of maven
        MAVEN_HOME = tool 'Maven 3.8'
        MAVEN_EXECUTABLE = "${MAVEN_HOME}/bin/mvn"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Maven home: ${MAVEN_HOME}"
                    echo "Maven executable: ${MAVEN_EXECUTABLE}"
                    
                    // log version of maven
                    bat "\"${MAVEN_EXECUTABLE}\" --version"

                    // build projet using maven
                    bat "\"${MAVEN_EXECUTABLE}\" clean package -nsu -DskipMunitTests"
                }
            }
        }

        stage('Test') {
            steps {
                // test project
                bat "\"${MAVEN_EXECUTABLE}\" clean test -nsu"
            }
        }

        stage('Deploying to cloudhub') {
            steps {
                // pdeploiong on cloudhub
                bat "\"${MAVEN_EXECUTABLE}\" clean deploy -DskipMunitTests -DmuleDeploy"
            }
        }
    }

    post {
        success {
            echo 'Prject is succeffuly deployed'
        }

        failure {
            echo 'deployement failled'
        }
    }
}
