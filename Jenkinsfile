pipeline {
  agent any
  stages {
    stage('START') {
      steps {
        bat 'echo "starting servers..."'
      }
    }
    stage('StartServers') {
      parallel {
        stage('Grafana') {
          when { allOf { expression { params.CHOICE ==~ /(Start)/ }; expression { return params.Grafana } }}
          steps {
            build 'startserver-Grafana'
          }
        }
        stage('Influxd') {
          when { allOf { expression { params.CHOICE ==~ /(Start)/ }; expression { return params.Influxd } }}
          steps {
            build 'startserver-Influxd'
          }
        }
        stage('Prometheus') {
          when { allOf { expression { params.CHOICE ==~ /(Start)/ }; expression { return params.Prometheus } } }
          steps {
            build 'startserver-Prometheus'
          }
        }
        stage('ToscaExecution') {
          when { allOf { expression { params.CHOICE ==~ /(Start)/ }; expression { return params.ToscaCIRemoteExecutionService} }}
          steps {
            build 'startService-ToscaCIRemoteExecutionService'
          }
        }
        stage('DigiToyApplication') {
          when {allOf {expression { params.CHOICE ==~ /(Start)/ }; expression { return params.DigitalToyWebapplication } }}
          steps {
            build 'startApp-DigitalToyWebapplication'
          }
        }
      }
    }
    stage('StopServers') {
      parallel {
        stage('Grafana') {
          when {
            allOf {
              expression {
                params.CHOICE ==~ /(Stop)/
              }
              expression {
                return params.Grafana
              }
            }
          }
          steps {
            build job: 'stopProcess', parameters: [[$class: 'StringParameterValue', name: 'processToStop', value: "grafana-server.exe"]]
          }
		  /*steps {
					build job: "job2", parameters[string(name: "var", value: "${VAR})]
				}*/
        }
        stage('Influxd') {
          when {
            allOf {
              expression {
                params.CHOICE ==~ /(Stop)/
              }

              expression {
                return params.Influxd
              }

            }

          }
          steps {
            build job: 'stopProcess', parameters: [[$class: 'StringParameterValue', name: 'processToStop', value: "Influxd.exe"]]
          }
        }
        stage('Prometheus') {
          when {
            allOf {
              expression {
                params.CHOICE ==~ /(Stop)/
              }

              expression {
                return params.Prometheus
              }

            }

          }
          steps {
            build job: 'stopProcess', parameters: [[$class: 'StringParameterValue', name: 'processToStop', value: "Prometheus.exe"]]
          }
        }
        stage('ToscaExecution') {
          when {
            allOf {
              expression {
                params.CHOICE ==~ /(Stop)/
              }

              expression {
                return params.ToscaCIRemoteExecutionService
              }

            }

          }
          steps {
            build job: 'stopProcess', parameters: [[$class: 'StringParameterValue', name: 'processToStop', value: "ToscaCIRemoteExecutionService.exe"]]
          }
        }
        stage('DigiToyApplication') {
          when {
            allOf {
              expression {
                params.CHOICE ==~ /(Stop)/
              }

              expression {
                return params.DigitalToyWebapplication
              }

            }

          }
          steps {
            build job: 'stopProcess', parameters: [[$class: 'StringParameterValue', name: 'processToStop', value: "javaw.exe"]]
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
  parameters {
    choice(name: 'CHOICE', choices: ['Start', 'Stop'], description: 'Pick something')
    booleanParam(name: 'Grafana', defaultValue: true, description: 'Toggle this value')
    booleanParam(name: 'Influxd', defaultValue: true, description: 'Toggle this value')
    booleanParam(name: 'Prometheus', defaultValue: true, description: 'Toggle this value')
    booleanParam(name: 'ToscaCIRemoteExecutionService', defaultValue: false, description: 'Toggle this value')
    booleanParam(name: 'DigitalToyWebapplication', defaultValue: false, description: 'Toggle this value')
  }
}