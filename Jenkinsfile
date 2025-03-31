pipeline{
  agent any 

  stages{

    stage('Instalar dependencias'){
      steps{
        script {
          try {
            //Instalando dependencias
            echo 'Instalando dependencias...'
            sh 'npm install'
          }
          catch (Exception e) { 
            error('❌ Error en la etapa de instalación de dependencias.')
          }
        }
      }
    }

    stage('Pruebas'){
      steps{
        script {
          //Ejecutando pruebas
          echo 'Ejecutando pruebas...'
          sh 'npm test --silent=false'
        }
      }
    }

    stage('Iniciando el servidor'){
      steps{
        script {
          try {
            //Iniciando servidor
            echo 'Iniciando el servidor...'
            sh 'npm run start'
          }
          catch (Exception e) { 
            error('❌ Error en la etapa de inicialización de servidor.')
          }
        }
      }
    }

  }
}