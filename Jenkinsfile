pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
	            sh 'make deps'
          }
        }
        stage('Linter') {
            steps {
            sh 'make lint || true'
        	}
        }
        stage('Test') {
            steps {
              sh 'make test with test_xunit || true'
              step([$class: 'XUnitBuilder',
                  tresholds: [
                        [$class: 'SkippedTreshold', failureTreshold: '0'],
                        [$class: 'FailedTreshold', failureThreshold: '1'],
                  tools: [[$class: 'JUnitType', pattern: 'test_results.xml']]]
            }
        }
      }
  }

}
