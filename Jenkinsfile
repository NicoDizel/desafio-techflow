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

    stage('Iniciando el servidor'){
      steps{
        script {
          try {
            //Iniciando servidor
            echo 'Iniciando el servidor...'
            sh 'node run dev'
          }
          catch (Exception e) { 
            error('❌ Error en la etapa de inicialización de servidor.')
          }
        }
      }
    }

  }
}