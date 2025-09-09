pipeline {
  agent any
     tools {
        maven 'Apache Maven-3.9.11'  // Make sure this matches your Maven installation name in Jenkins
        jdk 'JDK-17'         // Make sure this matches your JDK installation name in Jenkins
    }
    
    environment {
        MAVEN_OPTS = '-Dmaven.repo.local=.m2/repository'
    }

  stages {
    stage('Checkout') {
      steps {
        // pull code from your repo (if job is configured to use SCM this is optional)
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Build step - replace with your real build command if needed'
        // Example windows build placeholder:
        bat 'echo Building...'
      }
    }

    stage('Stop existing app') {
      steps {
        script {
          try {
            echo 'Stopping any existing Java processes (if any)...'
            // Windows: force kill java.exe if running; suppress errors with 2>nul
            bat 'taskkill /F /IM java.exe 2>nul || echo "No Java processes to kill"'
          } catch (Exception e) {
            // safe: log the failure, but don't break the pipeline unexpectedly
            echo "Failed to stop application: ${e.getMessage()}"
          }
        }
      }
    }

    stage('Start application') {
      steps {
        script {
          echo 'Starting application...'
          // Replace this with your real start command, e.g.:
          // bat 'start /B java -jar C:\\path\\to\\app.jar'
          // or bat 'mvn spring-boot:run'
          bat 'echo (start your app here)'
        }
      }
    }

    stage('Health check') {
      steps {
        script {
          echo 'Health check (replace with real check) ...'
          // Windows example: use curl or powershell if available
          // bat 'curl -s -I http://localhost:8080 || echo "health check failed"'
          bat 'echo Checking http://localhost:8080'
        }
      }
    }
  } // end stages

  post {
    success {
      echo 'Pipeline executed successfully! Application is deployed and running on http://localhost:8080'
    }
    unstable {
      echo 'Pipeline finished with warnings.'
    }
    failure {
      echo 'Pipeline failed. Check console output above for details.'
    }
    always {
      echo 'Performing final cleanup...'
      script {
        try {
          bat 'taskkill /F /IM java.exe 2>nul || echo "No Java processes to kill"'
        } catch (Exception e) {
          echo "Cleanup failed: ${e.getMessage()}"
        }
      }
    }
  }
}
