# Otros Comandos git avanzados para colaborar
Comandos github necesarios para colaborar y tener buenas prácticas.

```bash
git pull --rebase <remote> <branch>
```
Realizando un pull con el argumento `--rebase` nos aseguramos que nuestros cambios queden en la parte superior del histórico de commits evitando típicos commits de "Merged branch 16.0 into 16.0-xxxx"

```bash
git cherry-pick <commit>
```
Recrea el commit/s mencionados en el comando sobre la rama actual, no copies y pegues tus cambios haz un cherry-pick. Muy útil cuando tenemos que hacer un forward o backward de un cambio en un repositorio.
