pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'mvn -B -DskipTests clean package'
      }
    }

    stage('Test') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          archiveArtifacts 'target/*.jar'
        }

      }
      steps {
        bat 'mvn test'
      }
    }

    stage('Site') {
      steps {
        bat 'mvn site'
      }
    }

    stage('Sonar') {
      parallel {
        stage('Sonar') {
          agent any
          environment {
            SONAR_TOKEN = 'e30762a883f108b2e9244959f3beb2e9a8d432f8'
          }
          steps {
            bat 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=KarimJesusGalvez_m5-spring-jenkins'
          }
        }

        stage('') {
          steps {
            jacoco()
          }
        }

      }
    }

  }
  tools {
    maven 'maven3.8.3'
    jdk 'jdk17'
  }
}