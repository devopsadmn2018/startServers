pipeline {
  agent any
  stages {
    stage('Servers') {
      parallel {
        stage('Servers') {
          steps {
			parallel (
				{build 'startserver-Influxd'},
				{build 'startserver-Prometheus'},
				{build 'startserver-Grafana'}
			)	
          }
        }
        stage('Application') {
          steps {
            build 'startApp-DigitalToyWebapplication'
          }
        }
        stage('Service') {
          steps {
            build 'startService-ToscaCIRemoteExecutionService'
          }
        }
      }
    }
  }
}