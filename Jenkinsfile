pipeline {
    agent any 

    environment {
        NODE_VERSION = '18'
        PATH = "C:\\Program Files\\nodejs;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "📥 Clonando el repositorio..."
                checkout scm
            }
        }

        stage('Install') {
            steps {
                script {
                    try {
                        echo "⚙️ Instalando dependencias..."
                        bat 'npm install'
                        bat 'npm run build'
                    } catch (Exception e) {
                        error("❌ Error en la etapa de Install/Build")
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        echo "🧪 Ejecutando pruebas..."
                        bat 'npm run test'
                    } catch (Exception e) {
                        error("❌ Error en la etapa de Test")
                    }
                }
            }
        }

        stage('Validar servidor') {
            steps {
                script {
                    echo "🚀 Iniciando servidor..."
                    // Inicia el servidor en segundo plano
                    bat 'start /B npm start'
                    
                    // Esperar un momento para que el server levante
                    sleep(time: 5, unit: 'SECONDS')

                    echo "🔎 Verificando respuesta de la API..."
                    // Hacemos un request a localhost (suponiendo puerto 3000)
                    def response = bat(script: 'curl -s -o nul -w "%{http_code}" http://localhost:3000/users', returnStdout: true).trim()
                    
                    if (response != '200') {
                        error "❌ La API no respondió correctamente. Código HTTP: ${response}"
                    } else {
                        echo "✅ La API respondió correctamente (HTTP 200)"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completado con éxito"
        }
        failure {
            echo "❌ El pipeline ha fallado"
        }
    }
}