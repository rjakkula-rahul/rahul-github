pipeline {

  agent any

  parameters {
    string defaultValue: '', description: 'Test Name', name: 'TEST_NAME', trim: false
  }

  stages {
    stage('run tests') {
      steps {
        script {
          def optionalParameters = ""
          if (params.TEST_NAME != null) {
            optionalParameters += " -Dtest=" + params.TEST_NAME
          }
          sh "${mvnHome}/bin/mvn clean test -e -Dgroups=categories.dbd" + optionalParameters
        }
      }
    }
    ...
  }
  ...
}
