# Comandos de Git
## Intro [top ↑](#)
Comandos para establecer la configuración inicial, establecer un usuario y su email: 
```bash
git config --global user.name “nombreUsuario”
git config –global user.email “nombreUsuario@email.com”
```

## Git init [top ↑](#)
```bash
git init
```
El comando `git init` crea un nuevo repositorio de Git y puede utilizarse para convertir un proyecto existente y sin versión en un repositorio de Git o inicializar un nuevo repositorio vacío.

Si queremos hacer que en un directorio de trbabajo git ignore alguno archivos (que no queremos actualizar) podemos crear un archivo `.gitignore` y añadir en él el nombre de los archivos/directorios que queramos que git ignore. 

Ejemplo de archivo `.gitignore` para un repo de un backend hecho con pyhton: 
```
# Bytecode y caché
__pycache__/
*.py[cod]
*.pyo

# Entornos virtuales
.venv/
env/
venv/

# Configuración de entorno local
.env

# Archivos temporales / de sistema
.DS_Store
Thumbs.db

# Archivos de testing/coverage (opcional)
coverage/
htmlcov/
.tox/
pytest_cache/
.cache/

# Compilaciones (si usas Cython o similares)
build/
dist/
*.egg-info/

# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
dist
dist-ssr
*.local

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
*.swp
*.sublime*
```

## Git add [top ↑](#)
```bash
git add
```

El comando git add añade un cambio del directorio de trabajo en el entorno de ensayo: 
```bash
git add nombre_fichero
```

Si hacemos: 
```bash
git add .
```

Se añadirán todos los cambios pendientes. 

## Git commit [top ↑](#)
```bash
git commit -m
```

El comando git commit guardará todos los cambios hechos en la zona de montaje o área de preparación (`staging area`), junto con una breve descripción del usuario, en un "commit" al repositorio local. Puedes pensar en un commit como una captura de tu proyecto, donde se crea una nueva versión de ese proyecto en el repositorio actual. 

Con `-m` podemos especificar a continuación un mensaje de información sobre el commit, entre comillas. Es obligatorio. Si no se pone nos saldrá un molesto mensaje. 

## Git log [top ↑](#)
```bash
git log
```

El comando git log permite visualizar el historial de los commit, filtrarlo y buscar cambios específicos. Tiene muchas opciones para poder filtrar los resultados o estilizar su visualización. Por ejemplo:
```bash
git log --graph --decorate --all –oneline
```

Nos mostrará el historial de commits compactado, solo con la parte final del hash de cada commit. 

## Poner un alias [top ↑](#)
Con `git config --global alias.nombre_alias "comando"`, podemos poner un alias a un comando que queramos reutilizar sin necesidad de memorizar todo el comendo. Por ejemplo, podemos poner un alias al comando anterior: 
```bash
git config --global alias.tree "log --graph --decorate --all --oneline"
```

## Git status [top ↑](#)
```bash
git status
```

El comando git status muestra el estado actual de la `working directory` y de la staging area, permitiendo ver que archivos modificados se han añadido a la staging area, que archivos modificados no han sido añadidos a la staging area y que archivos no se rastrean en el repository.

## Git checkout [top ↑](#)
```bash
git checkout
```

El comando git checkout es una herramienta versátil que se utiliza principalmente para cambiar entre ramas, deshacer cambios en el área de trabajo y moverse a diferentes puntos en el historial del repositorio.

Supongamos que has hecho cambios en un archivo y deseas deshacerlos para volver a la versión anterior. Puedes utilizar `git checkout` seguido del nombre del archivo: 
```bash
git checkout archivo_modificado.txt 
```

**Deshacer todos los cambios en el área de trabajo:**
```bash
git checkout .
```

**Para realizar un checkout a un commit específico:**
```bash
git checkout id-del-commit-específico
```

**Para realizar checkout a una rama existente, ejecuta el comando:**
```bash
git checkout NOMBRE-DE-LA-RAMA
```

**Checkout a una rama nueva:**
```bash
git checkout -b NOMBRE-DE-LA-RAMA-NUEVA
```

## Git reset [top ↑](#)
```bash
git reset
```

El comando git reset se utiliza en Git para deshacer cambios en el repositorio y modificar la posición del puntero `HEAD`. 

**Deshacer cambios en el área de preparación (staging)**:
Supongamos que has agregado algunos archivos al área de preparación (staging) usando git add, pero ahora deseas deshacer esos cambios y volver a dejar los archivos sin preparar. Puedes utilizar `git reset` con la opción `--mixed` o sin ninguna opción para lograrlo. Por ejemplo: 
```bash
git reset HEAD archivo.txt
```

Este comando eliminará `archivo.txt` del área de preparación, pero los cambios en el archivo permanecerán en tu directorio de trabajo.

**Deshacer cambios en el área de preparación y en el directorio de trabajo**:
Si deseas deshacer los cambios en el área de preparación y también en el directorio de trabajo (es decir, eliminar los cambios que hiciste), puedes usar `git reset` con la opción `--hard`. Por ejemplo: 
```bash
git reset --hard HEAD
```

Este comando deshará todos los cambios en el área de preparación y en el directorio de trabajo, restaurando todo al estado en el que se encuentra el último commit.

**Deshacer commits y mover el puntero HEAD**:
```bash
git reset --soft HEAD~1
```

Este comando moverá el puntero HEAD al commit anterior (`HEAD~1`), manteniendo los cambios de ese commit en el área de preparación y en el directorio de trabajo.

**reflog**:
Si la cagamos con un git reset `--hard`. Aún tenemos opción a recuperar el trabajo empleando el comando: 
```bash
git reflog 
```

Aquí podremos ver el historial de TODOS los cambios con sus referencias (los reseteados también). De este log podemos recuperar la referencia (id) a los cambios resetados con git reset, si volvemos a hacer un reset `--hard` a sus id. 

## Git diff [top ↑](#)
```bash
git diff
```

Con este comando mostraremos los cambios que se han realizado en el directorio de trabajo siempre que se hayan realizado cambios sin haber hecho commit.  

## Git tag [top ↑](#)
```bash
git tag
```

El comando `git tag` se utiliza en Git para agregar, mostrar y manipular etiquetas (tags), que son identificadores asociados con puntos específicos en el historial de un repositorio Git.

**Crear una etiqueta ligera**:
```bash
git tag nombre_etiqueta
```

**Crear una etiqueta anotada**:
Una etiqueta anotada es similar a una etiqueta ligera, pero además puede contener información adicional como el nombre del autor, la fecha y un mensaje asociado. Para crear una etiqueta anotada, puedes utilizar el siguiente comando: 
```bash
git tag -a nombre_etiqueta -m "Mensaje asociado a la etiqueta"
```
**Mostrar etiquetas:**
```bash
git tag 
```
**Mostrar información detallada de una etiqueta**:
```bash
git show nombre_etiqueta 
```
**Eliminar etiquetas**:
```bash
git tag -d nombre_etiqueta 
```
También podremos movernos con checkout a una versión indicando su tag en vez de su id. 

## Git branch [top ↑](#)
```bash
git branch 
```
El comando git branch en Git se utiliza para listar, crear y eliminar ramas en tu repositorio.

**Listar ramas**:
```bash
git branch 
```
Esto mostrará todas las ramas disponibles en tu repositorio y resaltará la rama actual con un asterisco (*).

**Crear una nueva rama**:
```bash
git branch nombre_rama_nueva
```

**Eliminar una rama**:
```bash
git branch -d nombre_rama_nueva
```

Si la rama contiene cambios que aún no se han fusionado en otra parte del proyecto, Git no permitirá eliminarla. En ese caso, puedes forzar la eliminación utilizando: 
```bash
$ git branch -D
```

**Renombra la rama localmente**: 
Utiliza el comando git branch `-m` seguido del nombre actual de la rama y el nuevo nombre que deseas asignarle. Por ejemplo, si deseas renombrar una rama llamada `feature` a `nueva_feature`, puedes hacerlo de la siguiente manera:
```bash
git branch -m feature nueva_feature
```

Desde la rama “master” podemos hacer esto sin tener que cambiar de rama para cambiar su nombre a “main”: 
```bash
git branch -m main
```

## Git switch [top ↑](#)
```bash
git switch
```
Para cambiar entre ramas y crear nuevas ramas de forma más intuitiva. 

**Cambiar entre ramas**:
```bash
git switch otra_rama
```

**Crear y cambiar a una nueva rama**:
```bash
git switch -c nueva_rama
```

**Deshacer cambios en el área de trabajo**:
```bash
git switch --  (similar a git checkout)
```

**Crear y cambiar a una nueva rama basada en otra rama**:
```bash
git switch -c nueva_rama rama_base
```

Este comando creará una nueva rama llamada nueva_rama basada en rama_base y cambiará a ella.

**Cambiar a un commit específico**:
```bash
git switch <hash_del_commit>
```

Este comando cambiará a un estado temporal basado en el commit con el hash especificado.

**Diferencias entre git switch y git checkout**:
Git switch y git checkout son dos comandos de Git que se utilizan para cambiar entre ramas (branches) o puntos en el historial del repositorio. A partir de Git 2.23, git switch se introduce como un comando más seguro y específico para cambiar entre ramas, mientras que git checkout tiene una funcionalidad más amplia que también incluye la capacidad de cambiar entre ramas, pero también se utiliza para otras tareas como deshacer cambios en archivos, revisar commits específicos, etc.

Aquí están las principales diferencias entre git switch y git checkout:

_Propósito principal:_
- `git switch`: Está diseñado específicamente para cambiar entre ramas.
- `git checkout`: Tiene una funcionalidad más amplia y se utiliza para varias operaciones, como cambiar entre ramas, deshacer cambios en archivos, revisar commits específicos, etc.

_Seguridad:_
- `git switch`: Es más seguro en el sentido de que evita cambiar accidentalmente a un estado en el que se puedan perder cambios no guardados.
- `git checkout`: Puede cambiar el estado del directorio de trabajo y el índice de Git, lo que puede conducir a la pérdida de cambios no guardados si no se tiene cuidado.

_Comportamiento predeterminado:_
- `git switch`: No cambia archivos modificados en el directorio de trabajo o el índice de Git a menos que sea seguro hacerlo.
- `git checkout`: Puede cambiar archivos modificados en el directorio de trabajo o el índice de Git, lo que puede llevar a la pérdida de cambios no guardados.

## Git merge [top ↑](#)
```bash
git merge
```
Se utiliza para combinar los cambios de una rama con otra rama activa. 

**Fusionar una rama con la rama actual:**
Supongamos que estás en la rama main y deseas fusionar los cambios de una rama llamada `nueva_funcionalidad` en la rama actual (main). Para hacer esto, primero, **asegúrate de estar en la rama en la que deseas fusionar los cambios** y luego ejecuta el siguiente comando: 
```bash
git merge nueva_funcionalidad
```

**Fusionar con confirmación automática:**
Si Git puede fusionar automáticamente los cambios sin conflictos, lo hará y creará un nuevo commit de fusión. No se requerirá ninguna intervención del usuario. Por ejemplo, si no hay conflictos entre la rama actual y la rama que estás fusionando: 
```bash
git merge otra_rama
```

**Fusionar con conflictos:**
En ocasiones, puede haber conflictos entre los cambios en la rama actual y la rama que estás intentando fusionar. Git detendrá el proceso de fusión y te pedirá que resuelvas estos conflictos manualmente. Después de resolver los conflictos, debes agregar los archivos modificados y crear un nuevo commit de fusión. Por ejemplo: 
```bash
git merge otra_rama
```

En este punto, aparecerá un mensaje de conflicto. Debes resolver los conflictos manualmente editando los archivos. Después de resolver los conflictos, añades los archivos modificados:
```bash
$ git add .
```

Finalmente, creas el commit de fusión:
```bash
git commit -m "Resolución de conflictos al fusionar otra_rama"
```

**Fusión no fast-forward:**
A veces, cuando fusionas una rama en otra, Git crea un nuevo commit de fusión, incluso si podría avanzar directamente el puntero de la rama sin crear un commit de fusión. Esto se llama "fusión no fast-forward". Puedes forzar la creación de un commit de fusión incluso en casos en los que Git podría avanzar directamente el puntero de la rama utilizando la opción `--no-ff`. Por ejemplo:
```bash
git merge --no-ff otra_rama
```

## Git stash [top ↑](#)
Se utiliza para almacenar temporalmente cambios locales sin confirmar, permitiéndote trabajar en otra tarea o cambiar de rama sin tener que confirmar los cambios actuales.

**Guardar cambios en el stash:**
Supongamos que has realizado algunos cambios en tus archivos, pero no estás listo para confirmarlos. Puedes usar git stash para guardar esos cambios en el stash. Por ejemplo:
```bash
git stash
```

**Guardar cambios con un mensaje descriptivo:**
Puedes agregar un mensaje descriptivo al stash para identificar fácilmente los cambios guardados. Por ejemplo:
```bash
git stash save "Cambios temporales para la corrección de errores"
```

**Ver lista de cambios en el stash:**
Puedes ver una lista de todos los cambios guardados en el stash utilizando el comando git stash list. Por ejemplo:
```bash
git stash list
```

**Aplicar cambios desde el stash:**
Puedes aplicar los cambios guardados en el stash de vuelta a tu directorio de trabajo utilizando git stash apply. Por defecto, este comando aplicará el último conjunto de cambios guardados en el stash. Por ejemplo:
```bash
git stash apply
```
Si deseas aplicar un stash específico, puedes usar el identificador del stash. Por ejemplo, si el stash tiene el identificador `stash@{2}`:
```bash
git stash apply stash@{2} 
```

**Aplicar y eliminar cambios del stash:**
Si deseas aplicar los cambios y eliminarlos del stash, puedes usar git stash pop. Por ejemplo: 
```bash
git stash pop
```

**Eliminar un cambio específico del stash:**
Si deseas eliminar un cambio específico del stash sin aplicarlo, puedes usar git stash drop. Por ejemplo, si deseas eliminar el stash identificado como `stash@{1}`:
```bash
git stash drop stash@{1}
```

Si no especificamos el stash, borrará todo lo que esté en stash.
