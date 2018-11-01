pipeline {
  agent any
  stages {
    stage('startserver') {
      steps {
        bat 'echo "starting servers..."'
      }
    }
    stage('Servers') {
      parallel {
        stage('Grafana') {
          steps {
            powershell 'cd C:\\Users\\ajawale\\WorkSpace\\grafana-5.3.0\\bin'
            powershell 'Start-Process grafana-server.exe'
          }
        }
        stage('Influxd') {
          steps {
            build 'startserver-Influxd'
          }
        }
        stage('Prometheus') {
          steps {
            build 'startserver-Prometheus'
          }
        }
        stage('ToscaExecution') {
          steps {
            build 'startService-ToscaCIRemoteExecutionService'
          }
        }
        stage('DigiToyApplication') {
          steps {
            build 'startApp-DigitalToyWebapplication'
          }
        }
      }
    }
    stage('End') {
      steps {
        echo 'echo "servers started..."'
      }
    }
  }
}