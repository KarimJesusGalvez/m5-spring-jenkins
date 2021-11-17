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
      steps {
        bat 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=KarimJesusGalvez_m5-spring-jenkins'
      }
    }

  }
  tools {
    maven 'maven3.8.3'
    jdk 'jdk17'
  }
}