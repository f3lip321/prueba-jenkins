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
                    
                    // Inicia el servidor de manera sincrónica (sin /B) para esperar a que se inicie correctamente
                    bat 'npm start &'

                    // Esperar un momento más para asegurarse de que el servidor esté completamente levantado
                    sleep(time: 10, unit: 'SECONDS')  // Aumenta el tiempo de espera si es necesario

                    echo "🔎 Verificando respuesta de la API..."
                    // Hacemos un request a las rutas de la API
                    def responseUsers = bat(script: 'curl -s -o nul -w "%{http_code}" http://localhost:3000/users', returnStdout: true).trim()
                    def responseUserId = bat(script: 'curl -s -o nul -w "%{http_code}" http://localhost:3000/users/1', returnStdout: true).trim()

                    if (responseUsers != '200' || responseUserId != '200') {
                        error "❌ La API no respondió correctamente. Respuestas HTTP: /users: ${responseUsers}, /users/1: ${responseUserId}"
                    } else {
                        echo "✅ La API respondió correctamente a todas las rutas."
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