pipeline {
  agent any
  stages {
    stage('Paso 1 Constructor App') {
      steps {
        echo 'Iniciamos la construccion de nuestra app'
        mail(subject: 'Iniciando la construccion de nuestra app', body: 'comienza la ejecucion', charset: 'UTF-8', from: 'gp1304@gmail.com', replyTo: 'gp1304@gmail.com', to: 'gp1304@gmail.com')
        timestamps() {
          echo 'Marca de tiempo inicial'
        }

        sh 'sh ejecutar_constructor_script.sh'
      }
    }

    stage('Prueba en Linux') {
      steps {
        echo 'Iniciando la prueba de Linux'
        sh 'sh ejecutar_test_para_linux.sh'
        sleep 5
        timestamps() {
          echo 'Finalizo la ejecucion de la prueba Linux'
        }

      }
    }

    stage('Despliegue en Produccion') {
      steps {
        echo 'Desplegando en Produccion'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'gp1304@gmail.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}