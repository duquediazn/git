
## Extra: GitFlow
> [Artículo de referencia](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

GitFlow es un flujo de trabajo de Git popularizado por _Vincent Driessen_ en su artículo [A Successful Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/). Proporciona una estructura y una serie de reglas para gestionar el flujo de desarrollo en proyectos que requieren un enfoque estructurado y bien definido para la gestión de ramas.

La idea principal detrás de GitFlow es dividir el proceso de desarrollo en varias ramas, cada una con un propósito específico. Las ramas principales en GitFlow son:
- `Master/Main`: Esta rama representa la versión de producción estable del proyecto. Normalmente, los commits en esta rama reflejan las versiones que se han lanzado.
- `Develop`: Esta rama es donde reside el desarrollo en curso. Es común que las ramas de características, correcciones de errores y otras ramas se fusionen con esta rama cuando están listas para ser probadas y eventualmente se integran en la rama master.
- `Feature branches`: Cada nueva característica se desarrolla en su propia rama de características. Estas ramas se derivan de la rama de desarrollo y se fusionan nuevamente en la rama de desarrollo una vez que la característica está completa.
- `Release branches`: Cuando se está preparando una nueva versión para lanzamiento, se crea una rama de lanzamiento desde la rama de desarrollo. Esta rama se utiliza para realizar pruebas finales, correcciones de errores de último minuto y preparar la versión para su lanzamiento. Una vez que la versión está lista, se fusiona en tanto la rama master como la rama de desarrollo.
- `Hotfix branches`: Si se descubre un error en la rama master que necesita ser corregido de inmediato, se crea una rama de hotfix desde la rama master. Una vez que se corrige el error, esta rama se fusiona tanto en la rama master como en la rama de desarrollo.

## Ejemplo de uso de GitFlow [top ↑](#)
Supongamos que tienes un repositorio de Git y deseas utilizar GitFlow para gestionar el flujo de trabajo. Aquí hay una secuencia de comandos típica que podrías seguir:

1. **Inicialización de GitFlow**
Primero, debes inicializar GitFlow en tu repositorio. Esto se hace una sola vez.
```bash
git flow init 
```

2. **Inicio de una nueva característica**
Supongamos que quieres trabajar en una nueva característica llamada "nueva-caracteristica".
```bash
git flow feature start nueva-caracteristica 
```

3. **Desarrollo de la característica**
Realiza tus cambios y commits en esta rama de características.
```bash
git add .
git commit -m "Agregando nueva característica" 
```

4. **Finalización de la característica**
Una vez que la característica está completa, finalízala. Esto fusionará la rama de características en la rama de desarrollo.
```bash
git flow feature finish nueva-caracteristica 
```

5. **Preparación de una nueva versión para lanzamiento**
Supongamos que estás listo para preparar una nueva versión para lanzamiento.
```bash
git flow release start 1.0.0 
```

6. **Correcciones finales y preparación para lanzamiento**
Haz las correcciones finales, actualiza el número de versión, etc.
```bash
$ git add . 
$ git commit -m "Correcciones finales para lanzamiento 1.0.0" 
```

7. **Finalización del lanzamiento**
Una vez que la versión está lista, finaliza el lanzamiento. Esto fusionará la rama de lanzamiento tanto en la rama master como en la rama de desarrollo.
```bash
git flow release finish 1.0.0 
```

8. **Manejo de hotfixes (correcciones rápidas)**
Si surge un error crítico en producción, puedes crear un hotfix branch.
```bash
git flow hotfix start hotfix-1.0.1
git add . 
git commit -m "Corrigiendo error crítico" 
git flow hotfix finish hotfix-1.0.1 
```
Esto es solo un ejemplo básico de cómo se utiliza GitFlow. Dependiendo de las necesidades específicas de tu proyecto, es posible que necesites adaptarlo. Puedes echarle un vistazo a esta guía estructurada para usar en proyectos más complejos colaborativos y profesionales: [Git Workflow](./git_workflow.md)

