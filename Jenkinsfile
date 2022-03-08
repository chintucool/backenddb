pipeline {
   agent any
	
	tools {
      maven "maven3"
   }

   options(){
    timestamps()
  }
   stages {
		stage('Checkout') {
            steps {
                checkout scm
            }
        }
      stage('Build') {
         steps {
            sh("mvn -Dmaven.test.failure.ignore=true clean install")
         }

         post {
            success {
		jacoco(
                        execPattern: '**/jacoco.exec',
                        classPattern: '**/classes',
                        sourcePattern: '**/src/main/java',
                        inclusionPattern: '**/*.java'
                )
            }
         }
      }
   }
}
