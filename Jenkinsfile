pipeline{
  agent any 

  stages{

    stage('Instalar dependencias'){
      try {
        //Instalando dependencias
        echo 'Instalando dependencias...'
        sh 'npm install'
      }
      catch (Exception e) { 
        error('❌ Error en la etapa de instalación de dependencias.')
      }
    }

    stage('Iniciando el servidor...'){
      try {
        //Instalando dependencias
        echo 'Iniciando el servidor...'
        sh 'node run dev'
      }
      catch (Exception e) { 
        error('❌ Error en la etapa de inicialización de servidor.')
      }
    }
  }


}