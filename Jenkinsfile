pipeline {
    agent any

    stages {
        stage('Preparación') {
            steps {
                echo 'Descargando el código fuente...'
            }
        }
        stage('Construcción (Build)') {
            steps {
                echo 'Construyendo la imagen de Django...'
            }
        }
        stage('Pruebas (Test)') {
            steps {
                echo 'Ejecutando pruebas de la aplicación...'
            }
        }
        stage('Despliegue (Deploy)') {
            steps {
                echo 'Despliegue exitoso en el entorno de pruebas.'
            }
        }
    }
    
    post {
        success {
            echo '✅ ¡El Pipeline se ejecutó correctamente!'
        }
        failure {
            echo '❌ Hubo un error en el proceso.'
        }
    }
}