pipeline {
  agent any
  stages {
    stage('Servers') {
      parallel {
        stage('Servers') {
          steps {
			parallel(
				"Influx": {
							build 'startserver-Influxd'
						},
				"Prometheus": {
								build 'startserver-Prometheus'
							},
				"Grafana": {
							build 'startserver-Grafana'
						}
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