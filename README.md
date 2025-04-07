# 📄 Informe de Ejecución del Pipeline

## 🧾 Resumen

Este informe documenta los pasos realizados para configurar y ejecutar un pipeline de CI/CD como parte de la prueba **"Implementación de un pipeline de integración continua"**.

---

## 🛠️ Pasos Realizados

### 1. 🚀 Configuración Inicial del Proyecto

- Se inicializó un repositorio local y se vinculó con **GitHub**.
- Se realizó commit de una versión inicial del proyecto con los archivos base.

---

### 2. ⚙️ Configuración Básica de la API

- Se verificó el correcto funcionamiento de la API.
- Se detectó la ausencia del script para iniciar el servidor.
- Se añadió en el archivo `app.js` la siguiente instrucción para levantar el servidor:

```js
const PORT = 3000;
app.listen(PORT, () => console.log(`API is running on port ${PORT}`));
```

### 3. 🤖 Automatización Básica con Jenkins

- Se configuró **Jenkins** para automatizar el proceso de integración y despliegue continuo.
- Se utilizó la opción **"Pipeline script from SCM"** para obtener el pipeline directamente desde el repositorio.
- Configuración realizada:
  - **Branch**: `main`
  - **Script path**: `Jenkinsfile`
- Se verificó que Jenkins ejecutara correctamente las etapas definidas en el pipeline.

---

### 4. ✅ Ejecución de Pruebas Automatizadas

- Se añadió un nuevo stage llamado **"Test"** en el archivo `Jenkinsfile` para ejecutar pruebas automatizadas.
- Se realizaron modificaciones en el archivo `tests/app.test.js` para provocar una falla intencional y validar que el pipeline detectara errores correctamente.
- Se confirmó que el pipeline fallara al encontrar errores en las pruebas, asegurando la calidad del código antes de proceder al despliegue.

---

### 5. 📊 Reporte y Retroalimentación

- Se creó este archivo `REPORT.md` para documentar los pasos realizados y los problemas encontrados durante la implementación del pipeline.
- Se realizaron ajustes en el método **POST** de la API para generar un resultado acorde con las pruebas ejecutadas. Fue necesario instalar plugin de coverage y code coverage en jenkins. Lo ultimo fue modificar script test.
