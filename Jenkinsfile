pipeline {
  agent any
   parameters {
        choice(name: 'CHOICE', choices: ['Start', 'Stop'], description: 'Pick something')
        booleanParam(name: 'Grafana', defaultValue: true, description: 'Toggle this value')
        booleanParam(name: 'Influxd', defaultValue: true, description: 'Toggle this value')
        booleanParam(name: 'Prometheus', defaultValue: true, description: 'Toggle this value')
        booleanParam(name: 'ToscaCIRemoteExecutionService', defaultValue: false, description: 'Toggle this value')
        booleanParam(name: 'DigitalToyWebapplication', defaultValue: false, description: 'Toggle this value')
/*
		string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
        file(name: "FILE", description: "Choose a file to upload")*/
    }
  stages {
    stage('START') {
      steps {
        bat 'echo "starting servers..."'
      }
    }
	when { expression { params.CHOICE ==~ /(Stop)/ } }
    stage('Initiate') {
      parallel {
		
		stage('Grafana') {
        when { expression { return params.Grafana } }
		steps {
            build 'startserver-Grafana'
          }
        }
        stage('Influxd') {
		when { expression { return params.Influxd } }
          steps {
            build 'startserver-Influxd'
          }
        }
        stage('Prometheus') {
		when { expression { return params.Prometheus } }
          steps {
            build 'startserver-Prometheus'
          }
        }
        stage('ToscaExecution') {
		when { expression { return params.ToscaCIRemoteExecutionService } }
          steps {
            build 'startService-ToscaCIRemoteExecutionService'
          }
        }
        stage('DigiToyApplication') {
		when { expression { return params.DigitalToyWebapplication } }
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