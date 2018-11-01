pipeline {
  agent any
  stages {
    stage('START') {
      steps {
        bat 'echo "starting servers..."'
      }
    }
    stage('InitiateServer') {
      parallel {
        stage('Grafana') {
          steps {
            build 'startserver-Grafana'
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
	stage('InitiateApps') {
      parallel {
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
    stage('END') {
      steps {
        echo 'echo "servers started..."'
      }
    }
  }
}