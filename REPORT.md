# Informe de Ejecución del Pipeline

## Resumen

Este informe describe los pasos realizados para configurar y ejecutar el pipeline de CI/CD para la prueba "Implementación de un pipeline de integración continua".

## Pasos

1. **Configuración inicial del proyecto**

   - Se inicializó un repositorio local y se conectó a GitHub.
   - Se hizo commit de una versión inicial de los archivos

2. **Configuración básica de la API**

   - Se verifica el funcionamiento de la API, donde se detecta que faltaba la inclusión del script para levantar el servidor, como tambien incorporar en el archivo app.js, la siguiente instrucción:

   const PORT = 3000;
   app.listen(PORT, () => console.log(`API is running on port ${PORT}`));

3. **Automatización básica con Jenkins**

   - Se configuró Jenkins para automatizar el proceso de clonación del proyecto, instalación de dependencias y despliegue.
   - Se usó opción "Pipeline script from SCM"
   - Se usó nombre del Branch: main
   - Y para Script path: Jenkinsfile

4. **Ejecución de pruebas automatizadas**

   - Se modifica el pipeline para ejecutar pruebas preescritas automaticamente.

5. **Automatización básica con Jenkins**
   - Se configuró Jenkins para automatizar el proceso de construcción, prueba y despliegue.
   - Se usó opción "Pipeline script from SCM"
   - Se usó nombre del Branch: main
   - Y para Script path: Jenkinsfile
