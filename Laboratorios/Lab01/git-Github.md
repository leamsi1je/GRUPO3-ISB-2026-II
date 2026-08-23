 # Resumen: uso de Git y GitHub

 ## ¿Qué son Git y GitHub?

 Git es un sistema de control de versiones que permite registrar los cambios de un proyecto de manera local y volver a versiones anteriores sin perder el historial. GitHub es una plataforma en línea que almacena todos los cambios y modificaciones de los repositorios Git y facilita la colaboración mediante ramas, *commits*, *pull requests* y revisiones de código.

 ## Configuración inicial

 Después de instalar Git, se recomienda configurar el nombre y el correo que aparecerán en los *commits*:

 ```bash
 git config --global user.name "Tu Nombre"
 git config --global user.email "tu-correo@example.com"
 ```

 También es conveniente comprobar la configuración con `git config --list`. Para trabajar con GitHub, se puede autenticar la cuenta mediante GitHub CLI, un token de acceso personal o una clave SSH.

 ## Crear o descargar un repositorio

 Para convertir una carpeta local en un repositorio Git se utiliza:

 ```bash
 git init
 ```

 Si el proyecto ya existe en GitHub, se descarga con `git clone`:

 ```bash
 git clone https://github.com/usuario/repositorio.git
 cd repositorio
 ```

 Un repositorio puede tener un archivo `.gitignore` para indicar qué archivos no deben guardarse, como archivos temporales, dependencias o información privada.

 ## Flujo básico de trabajo

 El trabajo diario consiste en revisar los cambios, preparar los archivos, crear un *commit* y sincronizarlo con GitHub:

 ```bash
 git status
 git add nombre-del-archivo
 git commit -m "Describe brevemente el cambio"
 git push origin main
 ```

 `git status` muestra el estado del repositorio. `git add` coloca cambios en el área de preparación (*staging*), `git commit` guarda una versión en el historial y `git push` publica los *commits* en el repositorio remoto. Antes de comenzar a trabajar, conviene obtener los cambios más recientes con:

 ```bash
 git pull origin main
 ```

 Los *commits* deben ser pequeños y tener mensajes claros, porque así es más fácil entender el historial y detectar errores.

 ## Ramas y colaboración

 Las ramas permiten desarrollar una función o corregir un problema sin modificar directamente la rama principal:

 ```bash
 git switch -c nombre-de-la-rama
 git add .
 git commit -m "Agrega nueva funcionalidad"
 git push -u origin nombre-de-la-rama
 ```

 En GitHub, después de subir la rama, se crea un *pull request* hacia `main`. Allí otros integrantes pueden revisar el código, hacer comentarios y aprobar los cambios. Una vez terminada la revisión, el *pull request* se integra en la rama principal. Después de cambiar de nuevo a `main`, se actualiza la copia local:

 ```bash
 git switch main
 git pull origin main
 ```

 Para unir una rama localmente se puede usar `git merge nombre-de-la-rama`. Si dos cambios modifican la misma parte de un archivo, aparece un conflicto. En ese caso se deben revisar las marcas insertadas por Git, conservar la versión correcta, ejecutar `git add` y crear un *commit* para finalizar la resolución.

 ## Comandos útiles

 ```bash
 git log --oneline       # Consulta el historial resumido
 git diff                # Revisa cambios aún no preparados
 git branch              # Lista las ramas locales
 git remote -v           # Muestra los repositorios remotos
 git restore archivo     # Descarta cambios locales no guardados
 ```

 `git restore` debe utilizarse con cuidado, porque elimina los cambios indicados si todavía no se han guardado en un *commit*.

 ## Buenas prácticas

 - Trabajar en ramas descriptivas, por ejemplo `agrega-login` o `corrige-menu`.
 - Hacer *commits* frecuentes, pequeños y relacionados con un solo objetivo.
 - Actualizar la rama local antes de comenzar y revisar los cambios antes de hacer `push`.
 - No subir contraseñas, tokens, claves privadas ni archivos generados automáticamente.
 - Usar *pull requests* para revisar el código antes de integrarlo en `main`.
 - Mantener actualizado el archivo `README.md` con la información necesaria para ejecutar el proyecto.

 En resumen, Git administra el historial de cambios en el equipo local, mientras que GitHub permite compartir ese historial y coordinar el trabajo del equipo. Un flujo ordenado consiste en actualizar el repositorio, crear una rama, realizar cambios, guardarlos en *commits*, subir la rama y solicitar su revisión mediante un *pull request*.
