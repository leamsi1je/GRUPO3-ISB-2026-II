 # Resumen: uso de Git y GitHub

 ## ¿Qué son Git y GitHub?

 Git es un sistema de control de versiones que permite registrar los cambios de un proyecto de manera local y volver a versiones anteriores sin perder el historial. GitHub es una plataforma en línea que almacena todos los cambios y modificaciones de los repositorios Git y facilita la colaboración mediante ramas, *commits*, *pull requests* y revisiones de código.

 ## Instalacion
 Dependiendo del usuario que seas lo descargas de la manera indicada
 Linux:
 ```bash
 $ sudo apt-get install git
 ```
 macOs:
 ```bash
 $ brew install git
 ```
 Los usarios de windos lo pueden descargar desde git-scm.com.
 ## Configuración inicial

 Después de instalar Git, se recomienda configurar el nombre y el correo que aparecerán en los *commits*:

 ```bash
 git config --global user.name "Tu Nombre"
 git config --global user.email "tu-correo@example.com"
 ```

 Para trabajar con GitHub, se puede autenticar la cuenta mediante GitHub CLI, un token de acceso personal o una clave SSH.

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

 Un repositorio puede tener un archivo `.gitignore` para indicar qué archivos no deben guardarse, como archivos temporales  , dependencias o información privada.

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

 ## Inicia sesión en GitHub usando la terminal

 Para autenticar GitHub desde la terminal integrada de VS Code se recomienda instalar GitHub CLI y ejecutar:

 ```bash
 gh auth login
 ```

 Se debe seleccionar **GitHub.com**, elegir `HTTPS` o `SSH` y seguir las instrucciones del navegador. La autenticación puede comprobarse con:

 ```bash
 gh auth status
 ```

 También se puede iniciar sesión desde **Accounts** en VS Code. La cuenta autenticada permite clonar repositorios y publicar cambios sin introducir las credenciales en cada operación.

 ## Inicializa y confirma los cambios en VS Code

 1. Abre la carpeta del proyecto en VS Code y selecciona **Source Control**.
 2. Si aún no es un repositorio, selecciona **Initialize Repository**.
 3. Revisa los archivos modificados y utiliza el signo `+` o **Stage All Changes** para prepararlos.
 4. Escribe un mensaje descriptivo y selecciona **Commit** para confirmar los cambios.
 5. Si el proyecto todavía no existe en GitHub, selecciona **Publish to GitHub**, elige si será público o privado y confirma el nombre del repositorio.
 6. Para un repositorio que ya tiene remoto, selecciona **Push** o **Sync Changes** para enviar los *commits* a GitHub.

 ## Crear y cambiar de rama (Interfaz de usuario de VS Code)

 Selecciona el nombre de la rama en la barra de estado, normalmente aparece como `main`, y elige **Create new branch**. Escribe un nombre descriptivo, por ejemplo `agrega-login`, y confirma. VS Code cambia automáticamente a la nueva rama. Para cambiar de rama, vuelve a seleccionar el nombre actual y elige la rama deseada en la lista.

 Después de confirmar los cambios, selecciona **Publish Branch** para subir la rama a GitHub. Desde allí se puede crear un *pull request* para solicitar la revisión e integración de los cambios en `main`.

 ## Combinar y resolver conflictos (Interfaz de usuario de VS Code)

 Para combinar una rama, cambia a la rama que recibirá los cambios, normalmente `main`, abre el menú de ramas y selecciona **Merge Branch**. Escoge la rama que deseas combinar. Si existen conflictos, VS Code los mostrará en **Source Control** y en los archivos afectados.

 En cada conflicto se puede elegir **Accept Current Change**, **Accept Incoming Change** o **Accept Both Changes**. También es posible editar el archivo manualmente para conservar la solución correcta. Después de revisar el resultado, guarda el archivo, pulsa `+` para prepararlo y selecciona **Commit** para finalizar la combinación. Finalmente, usa **Push** o **Sync Changes** para publicar la resolución en GitHub.

 ## Envío automático después de cada confirmación (configuración de un solo clic)

 VS Code puede enviar los cambios automáticamente después de cada *commit*. Para activarlo, abre **Settings** con `Ctrl+,`, busca **Post Commit Command**, localiza `Git: Post Commit Command` y selecciona **Sync**.

 A partir de ese momento, VS Code intentará sincronizar el repositorio después de cada confirmación. Esta función debe usarse solo cuando los cambios estén revisados, ya que puede publicarlos inmediatamente en GitHub. Para trabajos colaborativos es preferible confirmar en una rama y revisar el *pull request* antes de combinarlo con `main`.

 En resumen, Git administra el historial de cambios en el equipo local, mientras que GitHub permite compartir ese historial y coordinar el trabajo del equipo. Un flujo ordenado consiste en actualizar el repositorio, crear una rama, realizar cambios, guardarlos en *commits*, subir la rama y solicitar su revisión mediante un *pull request*.

 ## Cómo redactar y escribir archivos `.md`

 Los archivos `.md` utilizan Markdown, un formato sencillo para organizar documentos con texto plano. Se recomienda escribir títulos con `#`, separar los párrafos con una línea en blanco, usar `-` para listas, colocar palabras importantes entre `**`, enlaces con `[texto](URL)` y comandos o nombres de archivos entre acentos graves. Por ejemplo:

 ```markdown
 # Título del documento

 ## Sección

 Este es un texto redactado de forma clara y ordenada.

 - Primer punto
 - Segundo punto

 Para más información, visita [GitHub](https://github.com).
 ```

 En VS Code se puede escribir y guardar el archivo con extensión `.md`, y observar su resultado con **Open Preview** o con `Ctrl+Shift+V`.
