# Git Workflow
## Tabla de contenidos
- [Parte I – Flujo sencillo personal (una sola rama main)](#parte-i--flujo-sencillo-personal-una-sola-rama-main-top-)
- [Parte II – GitFlow simple con rama develop (proyectos personales o estructurados)](#parte-ii--gitflow-simple-con-rama-develop-proyectos-personales-o-estructurados-top-)
- [Parte III – Flujo profesional con ramas protegidas y Pull Requests (PR)](#parte-iii--flujo-profesional-con-ramas-protegidas-y-pull-requests-pr-top-)

## Parte I – Flujo sencillo personal (una sola rama main) [TOP ⬆](#) 

### 1. Crear una nueva tarea o feature [TOP ⬆](#)

Para cada nueva funcionalidad o corrección, crea una rama desde main.  
Esto mantiene tu trabajo aislado y evita romper la rama principal.

Ejemplo:
```bash
git checkout -b feat/feature-name
```
Convenciones de nombres de ramas:
- feat/... → nuevas funcionalidades
- fix/... → correcciones de bugs
- refactor/... → cambios de refactorización
- style/... → cambios de estilo o CSS
- docs/... → documentación
- test/... → tests
- chore/... → configuración o mantenimiento

Ejemplos:
feat/add-navbar  
fix/form-validation  
docs/update-usage-guide

---

### 2. Hacer commits pequeños y temáticos [TOP ⬆](#)

Añade los cambios por partes lógicas:
```bash
git add -p
```
Haz commits siguiendo Conventional Commits:
```bash
git commit -m "<type>(<scope>): message"
```
- `<type>` → like feat, fix, refactor...
- `<scope>` → what part of the app changed (views, layout, navbar, etc.)
- `message` → clear and concise action
Ejemplo:
```bash
git commit -m "feat(view): apply Bootstrap to login form"
```
Ejemplos útiles:
feat(api): add login endpoint  
fix(cart): handle empty cart error  
docs(usage): update installation steps  

Buenas prácticas:
- cada commit → una idea
- mensajes claros, en presente
- commits fáciles de revisar y revertir

---

### 3. Limpiar el historial antes de compartir (opcional) [TOP ⬆](#)

Si tienes varios commits ruidosos (typos, logs, pruebas), puedes limpiarlos antes del push:
```bash
git rebase -i HEAD~N
```
Acciones típicas en rebase -i:
- pick → mantener commit
- reword → cambiar mensaje
- squash → unir commits
- drop → eliminar commit

Usa esto solo en commits que aún no has subido o en ramas privadas.

---

### 4. Revisar tu historial antes de mezclar [TOP ⬆](#)

Para visualizar los commits de forma clara:
```bash
git log --oneline --graph --decorate
```
Esto ayuda a verificar que:
- los commits son coherentes
- no hay restos de código temporal
- la rama se creó desde el punto correcto

---

### 5. Mezclar tu rama en main [TOP ⬆](#)


Cuando la feature esté lista:
```bash
git checkout main  
git pull origin main  
git merge feat/feature-name
```
Esto integra tus cambios manteniendo la historia clara.  
Evita reescribir la historia de main (no uses rebase sobre main).

> Si usaste `rebase` en la rama feature después de haberla publicado, revisa antes el historial para evitar merge commits innecesarios.
---

### 6. Limpieza [TOP ⬆](#)
Después del merge:
```bash
git branch -d feat/feature-name
```
Elimina la rama local (seguro después de merge)

### 7. Subir a GitHub [TOP ⬆](#)

Después de integrar en main:
```bash
git push origin main
```
Si necesitas subir tu rama feature (backup, revisión, etc.):
```bash
git push -u origin feat/feature-name
```
---

#### 7.1. Force push seguro tras un rebase local (solo en ramas privadas)

Si usaste rebase para limpiar commits, tendrás que forzar el push:
```bash
git push --force-with-lease
```
Esto es más seguro que hacer `--force` porque solo sobreescribe la rama remota si nadie más ha subido cambios desde tu último fetch.

> Nunca uses esto en ramas compartidas.

> [Git Push - Doc oficial](https://git-scm.com/docs/git-push)
---

### 8. Versionado con etiquetas (opcional) [TOP ⬆](#)

Para marcar versiones del proyecto:
```bash
git checkout main  
git pull origin main  
git tag -a v1.0.0 -m "First stable release" 
git push origin main 
git push origin v1.0.0
```
Recomendaciones:
- usa Semantic Versioning (v1.0.0, v1.1.0, v2.0.0)
- usa etiquetas anotadas (-a)
- crea tags siempre sobre commits estables en main

> [Basic Tagging - Doc oficial](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
---

### Cheat Sheet – Flujo personal sencillo [TOP ⬆](#)
```bash
# 1. Crear rama:
git checkout -b feat/some-feature

# 2. Trabajar y hacer commits:
git add -p
git commit -m "feat(scope): message"

# 3. (Opcional) Limpiar commits:
git rebase -i HEAD~N

# 4. Volver a main:
git checkout main

# 5. Actualizar main:
git pull origin main

# 6. Mezclar:
git merge feat/some-feature

# 7. Subir:
git push origin main

# 8. Borrar rama:
git branch -d feat/some-feature

# 9. (Opcional) Tag:
git tag -a v1.0.0 -m "msg"
git push origin v1.0.0
```

  
## Parte II – GitFlow simple con rama develop (proyectos personales o estructurados) [TOP ⬆](#)

Este flujo añade una rama develop para separar:
- main → versiones estables  
- develop → trabajo en progreso

Es útil cuando el proyecto crece o quieres practicar un flujo más profesional sin complicaciones.

---

### 1. Preparar el entorno de trabajo [TOP ⬆](#)

Asegúrate de que develop está actualizado:
```bash
git checkout develop  
git pull origin develop
```
Si aún no tienes develop (solo en proyectos nuevos):
```bash
git checkout -b develop  
git push -u origin develop
```
---

### 2. Crear una nueva feature desde develop [TOP ⬆](#)

Nunca trabajes directamente en develop.  
Crea una rama por feature:
```bash
git checkout -b feat/some-feature
```
La idea es:  
main → estable  
develop → acumulación de features  
feat/... → trabajo aislado

---

### 3. Hacer commits pequeños y claros [TOP ⬆](#)

Igual que en la Parte I:
```bash
git add -p  
git commit -m "feat(scope): message"
```
Ejemplo:
```bash
feat(products): add expiration status badge
```
---

### 4. Mantener tu rama al día mientras trabajas [TOP ⬆](#)

Si pasan días y develop avanza, trae los cambios **sin crear commits de merge**:
```bash
git fetch origin  
git rebase origin/develop
```
Esto mueve tus commits encima de los nuevos commits de develop, como si los hubieras escrito después.  
Ventajas:
- historial más limpio
- menos conflictos en el PR o en el merge final

---

### 5. Limpiar el historial (opcional) [TOP ⬆](#)

Si quieres dejar tus commits bonitos antes de integrar:
```bash
git rebase -i HEAD~N
```
Recuerda: 
- solo en tu rama privada.
- si haces rebase interactivo (modificas el historial), tendrás que forzar el push:
```bash
git push --force-with-lease
```
(siempre en la rama feature, nunca en develop)


---

### 6. Integrar la feature en develop [TOP ⬆](#)

Cuando termines la tarea:
```bash
git checkout develop  
git pull origin develop  
git merge feat/some-feature
```

---

### 7. Subir los cambios al remoto [TOP ⬆](#)

Actualiza develop en GitHub:
```bash
git push origin develop
```
Luego puedes borrar la rama feature:
```bash
git branch -d feat/some-feature  
git push origin --delete feat/some-feature
```

> Asegúrate de que la feature branch está 100% integrada antes de borrarla.

---

### 8. Crear un release (opcional) [TOP ⬆](#)

Cuando develop está listo para un release estable:
```bash
git checkout main  
git pull origin main  
git merge develop  
git tag -a v1.2.0 -m "Release: v1.2.0"  
git push origin main  
git push origin v1.2.0
```
---

### Cheat Sheet – GitFlow simple [TOP ⬆](#)
```bash
# 1. Actualizar develop:
git checkout develop  
git pull origin develop

# 2. Crear rama feature:
git checkout -b feat/some-feature

# 3. Trabajar y commitear:
git add -p  
git commit -m "feat(scope): message"

# 4. Mantener la rama actualizada:
git fetch origin  
git rebase origin/develop

# 5. Subir rama:
git push -u origin feat/some-feature

# 6. Opcional: si hiciste un rebase interactivo sobre tus commits:
git push --force-with-lease

# 7. Volver a develop y mezclar:
git checkout develop  
git pull origin develop  
git merge feat/some-feature

# 8. Subir cambios:
git push origin develop

# 9. Limpiar ramas:
git branch -d feat/some-feature  
git push origin --delete feat/some-feature

# 10. Release opcional:
git checkout main  
git pull origin main  
git merge develop  
git tag -a vX.Y.Z -m "Release message"  
git push origin main  
git push origin vX.Y.Z
```

## Parte III – Flujo profesional con ramas protegidas y Pull Requests (PR) [TOP ⬆](#)

Este es el flujo usado en equipos profesionales:
- main y develop están protegidas (no se puede hacer push directo)
- todo se integra mediante Pull Requests
- se usa rebase para mantener el historial limpio
- cada persona trabaja en su propia rama feature

Este flujo evita errores, mantiene control de calidad y garantiza que el historial sea claro.

---

### 1. Preparar develop antes de empezar a trabajar [TOP ⬆](#)

Debes asegurarte de que tu trabajo parte del estado más reciente:
```bash
git checkout develop  
git pull --rebase origin develop
```
Por qué usar `--rebase` aquí:
- evita commits _"Merge branch 'develop'…"_ innecesarios
- mantiene un historial lineal y limpio
- en equipos, facilita las revisiones

---

### 2. Crear una rama feature desde develop [TOP ⬆](#)
```bash
git checkout -b feat/some-feature
```
Cada feature, fix o cambio significativo debe tener su propia rama.

Ejemplos de nombres:
feat/expiration-api  
fix/login-flow  
docs/contributing-update

---

### 3. Trabajar y hacer commits claros [TOP ⬆](#)
```bash
git add -p  
git commit -m "feat(scope): implement expiration filtering"
```
Commit pequeños y temáticos → revisiones más fáciles y PR más limpios.

---

### 4. Mantener tu rama al día mientras trabajas (muy importante) [TOP ⬆](#)

Mientras trabajas, otros compañeros (o tú misma desde otras ramas) pueden subir cambios a develop.  
Para evitar conflictos en el PR:
```bash
git fetch origin  
git rebase origin/develop
```
Rebase “mueve” tus commits a la punta de develop, como si los hubieras escrito después.  
Esto minimiza conflictos y deja una historia limpia cuando abras el PR.

Si el rebase provoca conflictos:
- resuélvelos manualmente
- git add archivo
- git rebase --continue

---

### 5. Publicar tu rama feature en el remoto [TOP ⬆](#)
```bash
git push -u origin feat/some-feature
```
Si hiciste un rebase (normal o interactivo) sobre commits ya subidos y necesitas actualizar el PR:
```bash
git push --force-with-lease  
```
Nunca uses `--force` normal.  
Nunca fuerces sobre develop o main (están protegidas y romperías el flujo).

---

### 6. Abrir un Pull Request desde GitHub [TOP ⬆](#)

Cuando haces un push de una rama nueva al remoto, Git suele mostrar en la consola un mensaje como:
```bash
remote: Create a pull request for 'feat/some-feature' on GitHub by visiting:
https://github.com/usuario/repositorio/compare/feat/some-feature?expand=1
```
Ese enlace aparece automáticamente porque se ha detectado una rama nueva o una rama actualizada en el remoto.  
Si haces clic, te llevará directamente a la pantalla de creación de un Pull Request.

También verás un botón en GitHub llamado:  
**“Compare & pull request”**

Ambas rutas te llevan a la misma pantalla.

---

#### ¿Qué verás al abrir el PR?

GitHub te mostrará un formulario con:

1. Base branch → la rama donde quieres integrar el cambio  
   (normalmente develop en proyectos con GitFlow)

2. Compare branch → tu rama (feat/some-feature)

3. Un cuadro de texto para el título  
   Usa estilo Conventional Commits:
   - feat(api): add expiration range endpoint
   - fix(frontend): correct expiration param alignment
   - docs(contributing): restructure workflow guide

4. Un cuadro para la descripción  
   Explica brevemente:
   - qué problema solucionas  
   - qué cambios introduces  
   - si afecta a UX/UI  
   - pasos para probarlo (si aplica)

5. Un resumen visual de los commits y archivos modificados  
   Aquí puedes revisar si todo lo que aparece realmente pertenece a tu feature.

6. Una vista de los “diffs” (cambios de líneas)  
   Útil para detectar cosas que se colaron por error.

7. Un panel donde GitHub indica si hay conflictos  
   - “This branch has no conflicts with the base branch” → perfecto  
   - “This branch has conflicts” → hay que resolverlos antes de poder hacer merge

---

#### Consejos para un buen PR

- Haz PR pequeños y enfocados: cuanto más pequeños, más fáciles de revisar.
- Añade capturas si el cambio afecta a la interfaz.
- Si introduces lógica compleja, explica brevemente el porqué.
- Revisa siempre el diff antes de enviar el PR (evita sorpresas).

---

### 7. Revisiones, cambios y actualización del PR [TOP ⬆](#)

Si necesitas hacer cambios en la misma rama:

1. Edita el código
2. git add / git commit
3. git push

Si hiciste rebase durante la revisión:
```bash
git push --force-with-lease
```

> Esto actualiza el PR automáticamente.

#### 7.1. Traer un commit desde otra rama (`git cherry-pick`, opcional)
A veces un commit se hace en la rama equivocada, o necesitas traer solo un cambio específico sin mezclar toda la rama. Para esto sirve git cherry-pick.

**Ejemplos de uso típico:**
- Hiciste un fix en feat/x pero debería haber ido a develop.
- Hay un commit en hotfix/... que necesitas también en tu rama feature.
- Quieres recuperar un commit concreto sin traer el resto del historial.

**Cómo usarlo:**
1. Localiza el hash del commit que quieres traer:
```bash
git log --oneline
```
2. Cambia a tu rama actual (la que debe recibir el commit):
```bash
git checkout feat/some-feature
```
Aplica ese commit encima de tu rama:
```bash
git cherry-pick <hash>
```
Git copiará ese commit (solo ese) y lo aplicará como un commit nuevo en tu rama.

**Si aparecen conflictos:**
- Resuélvelos manualmente
```bash
git add .
git cherry-pick --continue
```

**Consejos:**
- No uses cherry-pick para copiar commits grandes (mejor un merge o rebase).
- Es muy útil para rescatar commits que quedaron “atrapados” en una rama equivocada.
- Ideal para corregir errores comunes sin romper el historial.

---

### 8. Merge del Pull Request [TOP ⬆](#)

El equipo usa normalmente “Squash & Merge”. Razones:

- deja un solo commit claro en develop
- evita commits intermedios ruidosos
- facilita revertir el cambio si fuese necesario
- mantiene el historial limpio

Después del merge:
- develop se actualiza en GitHub
- tu PR se cierra
- tu rama feature se puede borrar (local y remota)

---

### 9. Mantener tu entorno actualizado después del merge [TOP ⬆](#)
```bash
git checkout develop  
git pull origin develop
```
Esto sincroniza tu entorno local con el código aprobado en el PR.

Luego limpia:
```bash
git branch -d feat/some-feature  
git push origin --delete feat/some-feature
```
---

### 10. Flujo de releases con rama main protegida [TOP ⬆](#)

Cuando develop está estable y probado, se prepara un release:
```bash
git checkout develop  
git pull origin develop  
git checkout -b release/v1.2.0  
git push origin release/v1.2.0
```

Abre un PR hacia main (GitHub).

Después de mergear el PR **hacia main**:
```bash
git checkout main  
git pull origin main  
git tag -a v1.2.0 -m "Release v1.2.0"  
git push origin v1.2.0
```
main queda actualizado, versionado y estable.

---

### Cheat Sheet – Flujo profesional con PR y ramas protegidas [TOP ⬆](#)
```bash
# 1. Actualizar develop:
git checkout develop  
git pull --rebase origin develop

# 2. Crear feature:
git checkout -b feat/some-feature

# 3. Trabajar:
git add -p  
git commit -m "feat(scope): message"

# 4. Mantener actualizada la rama:
git fetch origin  
git rebase origin/develop

# 5. Subir rama:
git push -u origin feat/some-feature

# 6. Opcional: si hiciste rebase (normal o interactivo) sobre commits ya subidos:
git push --force-with-lease
```

Cuando hayas terminado en tu rama y estés lista para añadir tus cambios a develop: 
**Abrir Pull Request → base: develop**

Después del merge del PR a develop:
```bash
# 7. Tras merge del PR:
git checkout develop  
git pull origin develop  
git branch -d feat/some-feature  
git push origin --delete feat/some-feature
```

Flujo de release (cuando develop está listo para versión estable):
```bash
# 8. Crear release branch:
git checkout develop  
git pull origin develop  
git checkout -b release/vX.Y.Z  
git push origin release/vX.Y.Z  
```

De nuevo PR (esta vez a main)
**Abrir Pull Request → base: main**

Después de mergear la release en main: 
```bash
git checkout main  
git pull origin main  
git tag -a vX.Y.Z -m "Release vX.Y.Z"  
git push origin vX.Y.Z
```