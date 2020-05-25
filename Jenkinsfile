pipeline{

    agent any

    tools{

        maven 'M2_HOME'
        jdk 'JAVA_HOME'
    }

    stages{

        stage('Clean Project'){

            steps{

                sh 'mvn clean install package'
            }

        }
    }
}