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

        stage('Deploy') { 
            steps { 
                script { 
                    try { 
                        echo "🚀 Desplegando aplicación..." 
                        bat 'start /B npm start'
                        echo "La aplicación se está ejecutando en segundo plano."
                        bat 'curl -s http://localhost:3000/users'
                        echo "La aplicación se ha desplegado correctamente."
                    } catch (Exception e) { 
                        error("❌ Error en la etapa de Deploy") 
                    } 
                } 
            } 
        }     
    }

    post {
        success {
            echo "✅ Pipeline completado con éxito"
            cobertura coberturaReportFile: 'coverage/cobertura-coverage.xml'
        }
        failure {
            echo "❌ El pipeline ha fallado"
        }
    }
}