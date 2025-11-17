
# Comandos de GitHub
## Intro – autentificación SSH en GitHub
Usando el protocolo SSH, te puedes conectar y autenticar con servicios y servidores remotos. Con las claves SSH puedes conectarte a GitHub sin necesidad de proporcionar el nombre de usuario y el personal access token en cada visita. También puedes usar una clave SSH para firmar confirmaciones.

Siguiendo estos artículos de GitHub podemos generar fácilmente una clave SSH:
- [Comprobar tus claves SSH existentes](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
- [Generación de una nueva clave SSH y adición al agente SSH](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Agregar una clave SSH nueva a tu cuenta de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

## Git remote [top ↑](#)
Para administrar las conexiones remotas a repositorios. Te proporciona información sobre los repositorios remotos que están vinculados a tu repositorio local y te permite agregar, ver y eliminar conexiones remotas. 

**Ver repositorios remotos vinculados:**
Puedes utilizar git remote sin argumentos para mostrar una lista de los nombres de los repositorios remotos vinculados a tu repositorio local. Por ejemplo:
```bash
git remote
```
Este comando mostrará una lista de los nombres de los repositorios remotos, como origin, que es el nombre predeterminado dado al repositorio remoto cuando clonas un repositorio.

**Ver detalles de un repositorio remoto específico:**
Si deseas obtener más detalles sobre un repositorio remoto específico, puedes usar git remote show seguido del nombre del repositorio remoto. Por ejemplo:
```bash
git remote show origin
```
Este comando mostrará información detallada sobre el repositorio remoto llamado origin, como las URL de fetch y push, las ramas que se están rastreando, etc.

**Agregar un nuevo repositorio remoto:**
Puedes agregar un nuevo repositorio remoto utilizando git remote add seguido del nombre que deseas darle al repositorio remoto y la URL del repositorio remoto. Por ejemplo:
```bash
git remote add upstream https://github.com/usuario/repositorio.git
```
Este comando agregará un nuevo repositorio remoto con el nombre upstream y la URL especificada. También se puede poner de esta forma: 
```bash
git remote add origin git@github.com:duquediazn/hello-git.git
```
En este caso, lo añadimos al repositorio remoto origin. De esta manera lo que estamos haciendo es emparejar nuestro repositorio en local sobre el que estemos trabajando con el repositorio creado en remoto en GitHub (hello-git.git, en este caso).

**Eliminar un repositorio remoto:**
Si necesitas eliminar un repositorio remoto que ya no necesitas, puedes utilizar git remote remove seguido del nombre del repositorio remoto que deseas eliminar. Por ejemplo:
```bash
git remote remove upstream
```
Este comando eliminará el repositorio remoto llamado upstream de tu configuración remota.

## Git push [top ↑](#)
**Para enviar los cambios locales confirmados a un repositorio remoto:**
Supongamos que estás trabajando en un proyecto colaborativo en GitHub y has realizado algunos cambios en tu repositorio local y has confirmado esos cambios con git commit. Ahora deseas enviar esos cambios al repositorio remoto en GitHub.
1.	Primero, asegúrate de estar en la rama correcta donde deseas enviar los cambios. Puedes verificarlo con git branch. 
2.	Ahora, para enviar tus cambios al repositorio remoto, utiliza git push seguido del nombre del repositorio remoto y la rama a la que deseas enviar los cambios. Por ejemplo, si tu repositorio remoto se llama "origin" (es el nombre por defecto que Git le da al repositorio remoto) y la rama se llama "main" (o cualquier otra rama que desees actualizar):
```bash
git push origin main
```
En este ejemplo, origin es el nombre del repositorio remoto y main es el nombre de la rama en el repositorio remoto. Esto enviará los cambios confirmados en tu rama local hacia la rama main del repositorio remoto.

Si tienes configurado un seguimiento de ramas (tracking branch), puedes simplemente utilizar git push sin especificar el repositorio remoto y la rama local, Git sabrá automáticamente dónde enviar los cambios. 

**Para configurar un seguimiento de ramas:**
El comando `git push -u` en Git es una forma de establecer una relación de seguimiento (tracking) entre una rama local y una rama remota. La opción `-u` significa `--set-upstream`, que se utiliza para configurar la rama remota como la rama de seguimiento predeterminada para la rama local.
Cuando ejecutas git push `-u`, estás indicando a Git que deseas enviar tus cambios locales a la rama remota y, al mismo tiempo, establecer una relación de seguimiento entre tu rama local y la rama remota. Ejemplo: 
```bash
git push -u origin main
```

## Git fetch [top ↑](#)
El comando `git fetch` en Git se utiliza para recuperar cambios del repositorio remoto a tu repositorio local. A diferencia de git pull, que fusiona automáticamente los cambios recuperados con tu rama local, git fetch solo recupera los cambios del repositorio remoto y los almacena en tu repositorio local, sin fusionarlos automáticamente. Esto te permite revisar los cambios antes de incorporarlos a tu trabajo local.

## Git pull [top ↑](#)
El comando git pull en Git se utiliza para recuperar los cambios del repositorio remoto y fusionarlos automáticamente con tu rama local. Básicamente, git pull realiza dos operaciones en una:
1.	Recuperación de cambios del repositorio remoto: Primero, git pull ejecuta git fetch para recuperar todos los cambios del repositorio remoto a tu repositorio local, actualizando las referencias locales con la información más reciente del repositorio remoto.
2.	Fusión de cambios: Después de recuperar los cambios del repositorio remoto con git fetch, git pull automáticamente fusiona esos cambios con tu rama local. Utiliza la estrategia de fusión predeterminada de Git para combinar los cambios del repositorio remoto con tu trabajo local. Dependiendo de la configuración de tu repositorio y las preferencias de fusión, Git puede realizar una fusión rápida (fast-forward merge) o una fusión recursiva (recursive merge) para combinar los cambios. Si hay conflictos entre los cambios locales y remotos, Git intentará fusionarlos de la mejor manera posible y marcará los conflictos para que los resuelvas manualmente. 

Sintaxis: 
```bash
git pull origin mi_rama_remota
```
- `origin` es el nombre del repositorio remoto del que deseas recuperar los cambios.
- `mi_rama_remota` es el nombre de la rama remota de la que deseas obtener los cambios.

## Git clone [top ↑](#)
Comando de Git que se utiliza para crear una copia exacta (clon) de un repositorio Git existente en un nuevo directorio local.
Cuando ejecutas git clone, Git:
1.	Descarga todos los archivos y el historial de versiones del repositorio remoto.
2.	Crea una copia local del repositorio en tu máquina.
3.	Configura automáticamente el repositorio remoto original como "origin", lo que te permite enviar cambios de vuelta al repositorio remoto si tienes permisos adecuados.

Aquí tienes un ejemplo de cómo usar git clone:
```bash
git clone https://github.com/ejemplo/Repositorio.git
```
Después de completar el clonado, puedes comenzar a trabajar con el repositorio localmente, realizar cambios, confirmarlos y, si tienes permisos, enviarlos de vuelta al repositorio remoto utilizando comandos como git add, git commit y git push.

## Fork y pull request [top ↑](#)
En GitHub, un `fork` es una copia de un repositorio de código almacenado en la cuenta de otro usuario en GitHub. Cuando haces un fork de un repositorio, GitHub crea una copia exacta del repositorio original en tu propia cuenta. Esta copia incluye todo el historial de versiones, los archivos y las ramas del repositorio original.

Los forks son útiles en situaciones donde quieres contribuir a un proyecto sin tener permisos de escritura en el repositorio original. Al hacer un fork, puedes trabajar en tu propia copia del proyecto, realizar cambios, experimentar y probar nuevas ideas sin afectar el proyecto original.

Una vez que has hecho cambios en tu fork y estás satisfecho con ellos, puedes enviar una "solicitud de extracción" (`pull request`) al propietario del repositorio original. Esta solicitud de extracción notifica al propietario del repositorio original sobre los cambios que has realizado en tu fork y les da la opción de revisar, discutir y, finalmente, fusionar tus cambios en el repositorio original.

En resumen, un fork en GitHub te permite crear una copia personal de un repositorio en tu propia cuenta, lo que te permite colaborar y contribuir a proyectos de código abierto de manera efectiva.

**Ejemplo con capturas:**
![alt text](./images/image.png)
![alt text](./images/image-1.png)

Tras haber hecho el fork, podrás clonar el proyecto en local y trabajar sobre él. Una vez hayas hecho commit de los cambios y los hayas subido (mediante git push) a tu copia del repositorio podrás hacer un pull request para que esos cambios se puedan ver reflejados en el repositorio original. 

Antes de realizar un pull request, es conveniente hacer un sync fork con el repositorio original para tener nuestra copia actualizada. 

![alt text](./images/image-2.png)

Para realizar un PR (pull request):

![alt text](./images/image-3.png)
![alt text](./images/image-4.png)

Si no se detectan posibles conflictos: 

![alt text](./images/image-5.png)

En el repositorio original podemos ver cómo ha llegado la petición: 
![alt text](./images/image-6.png)

El usuario o usuarios del repositorio original podrán decidir qué hacer con la petición. Podrán aceptar o rechazarla, pedir cambios y hacer comentarios. Si se acepta la petición, el último paso será permitir el `merge`.
![alt text](./images/image-7.png)
![alt text](./images/image-8.png)

En el caso de que se detectase algún conflicto: 
![alt text](./images/image-9.png)

Podremos analizar y resolver el conflicto tanto en remoto como en local si hacemos un pull a nuestro equipo, dependerá de la complejidad del conflicto y de nuestra preferencia personal. 
