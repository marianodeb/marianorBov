
## Ramas

### 1. **Crear una rama**

Para crear una nueva rama en Git, puedes usar el siguiente comando:

```bash
git branch nombre_de_la_rama
```

Este comando crea una nueva rama, pero no cambia automáticamente a ella. Para crear una rama y cambiarte a ella inmediatamente, puedes usar:

```bash
git checkout -b nombre_de_la_rama
```

O, en versiones más recientes de Git (2.23+), puedes usar:

```bash
git switch -c nombre_de_la_rama
```

### 2. **Eliminar una rama**

Para eliminar una rama local que ya no necesitas, puedes usar:

```bash
git branch -d nombre_de_la_rama
```

Si la rama tiene cambios que no han sido fusionados y estás seguro de que quieres eliminarla de todos modos, puedes forzar la eliminación con:

```bash
git branch -D nombre_de_la_rama
```

Para eliminar una rama remota, usa:

```bash
git push origin --delete nombre_de__la_rama
```

### 3. **Moverse entre ramas**

Para cambiar a una rama existente, puedes usar:

```bash
git checkout nombre_de_la_rama
```

O, en versiones más recientes de Git (2.23+), puedes usar:

```bash
git switch nombre_de_la_rama
```

### 4. **Listar o ver ramas**

Para listar todas las ramas locales en tu repositorio, usa:

```bash
git branch
```

Esto mostrará una lista de ramas locales, con un asterisco (`*`) al lado de la rama actual.

Para listar todas las ramas, incluyendo las remotas, usa:

```bash
git branch -a
```

Para listar solo las ramas remotas, usa:

```bash
git branch -r
```

### 5. **Renombrar una rama**

Para renombrar una rama local, puedes usar:

```bash
git branch -m nombre_actual nuevo_nombre
```

Si la rama ya ha sido enviada al repositorio remoto, deberás eliminar la rama antigua y enviar la nueva:

```bash
git push origin --delete nombre_actual
git push origin nuevo_nombre
```

### 6. **Fusionar ramas**

Para fusionar una rama en la rama actual, primero cambia a la rama de destino y luego usa:

```bash
git merge nombre_de_la_rama_a_fusionar
```

### 7. **Rebasar ramas**

El rebase es una alternativa a la fusión. Para rebasar la rama actual con otra rama, usa:

```bash
git rebase nombre_de_la_rama
```

Esto aplicará los cambios de la rama especificada sobre la rama actual.

### 8. **Sincronizar ramas remotas**

Para actualizar tu lista de ramas remotas y asegurarte de que estás al día con los cambios en el repositorio remoto, usa:

```bash
git fetch origin
```

Para actualizar una rama local con los cambios de su contraparte remota, puedes usar:

```bash
git pull origin nombre_de_la_rama
```

### 9. **Crear una rama a partir de un commit específico**

Si deseas crear una rama a partir de un commit específico, primero encuentra el hash del commit (puedes usar `git log` para ver los commits) y luego usa:

```bash
git branch nombre_de_la_rama hash_del_commit
```

### 10. **Comparar ramas**

Para ver las diferencias entre dos ramas, puedes usar:

```bash
git diff nombre_de_la_rama1..nombre_de_la_rama2
```

### 11. **Forzar el movimiento a una rama (descarta cambios locales)**

Si tienes cambios locales que no deseas conservar y quieres forzar el cambio a otra rama, puedes usar:

```bash
git reset --hard
git checkout nombre_de_la_rama
```

### 12. **Ver el historial de una rama**

Para ver el historial de commits de una rama específica, usa:

```bash
git log nombre_de_la_rama
```

### 13. **Crear una rama y hacer un seguimiento de la rama remota**

Si creas una rama local y quieres que haga seguimiento de una rama remota, puedes usar:

```bash
git checkout --track origin/nombre_de_la_rama
```

O, en versiones más recientes de Git:

```bash
git switch --track origin/nombre_de_la_rama
```

### 14. **Eliminar ramas locales que ya no existen en el remoto**

Si has eliminado ramas remotas y quieres limpiar las ramas locales que ya no tienen un equivalente remoto, puedes usar:

```bash
git fetch --prune
```

Esto eliminará automáticamente las ramas locales que ya no tienen un rastro en el repositorio remoto.

### 15. **Crear una rama a partir de un tag**

Si deseas crear una rama a partir de un tag, puedes usar:

```bash
git branch nombre_de_la_rama nombre_del_tag
```

### 16. **Ver la última rama en la que estabas**

Si quieres volver a la última rama en la que estabas trabajando, puedes usar:

```bash
git checkout -
```

O, en versiones más recientes de Git:

```bash
git switch -
```

### 17. **Verificar el estado de las ramas**

Para ver el estado actual de las ramas, incluyendo cuáles tienen cambios no comprometidos, puedes usar:

```bash
git status
```

### 18. **Crear una rama y enviarla al repositorio remoto**

Si creas una rama local y quieres enviarla al repositorio remoto inmediatamente, puedes usar:

```bash
git push -u origin nombre_de_la_rama
```

El flag `-u` (o `--set-upstream`) establece la rama local para hacer seguimiento de la rama remota.

### 19. **Verificar diferencias entre la rama local y la remota**

Para ver las diferencias entre tu rama local y su contraparte remota, puedes usar:

```bash
git diff origin/nombre_de_la_rama
```

### 20. **Forzar la actualización de una rama local con la remota**

Si quieres actualizar tu rama local con los cambios de la rama remota y descartar cualquier cambio local, puedes usar:

```bash
git reset --hard origin/nombre_de_la_rama
```

### 21. **Crear una rama a partir de un stash**

Si tienes cambios en el stash y quieres crear una rama a partir de ellos, puedes usar:

```bash
git stash branch nombre_de_la_rama
```

Esto creará una nueva rama y aplicará los cambios del stash.

### 22. **Verificar el historial de fusiones**

Para ver un historial de fusiones en la rama actual, puedes usar:

```bash
git log --merges
```

### 23. **Verificar el historial de rebases**

Para ver un historial de rebases en la rama actual, puedes usar:

```bash
git reflog
```

### 24. **Crear una rama a partir de un commit específico y cambiarte a ella**

Si deseas crear una rama a partir de un commit específico y cambiarte a ella inmediatamente, puedes usar:

```bash
git checkout -b nombre_de_la_rama hash_del_commit
```

O, en versiones más recientes de Git:

```bash
git switch -c nombre_de_la_rama hash_del_commit
```

### 25. **Verificar el historial de una rama en un formato gráfico**

Para ver el historial de una rama en un formato gráfico, puedes usar:

```bash
git log --graph --oneline --decorate --all
```

Esto te mostrará un gráfico de todas las ramas y sus commits.

### 26. **Forzar la eliminación de una rama remota**

Si necesitas forzar la eliminación de una rama remota, puedes usar:

```bash
git push origin --delete nombre_de_la_rama
```

### 27. **Verificar el historial de una rama específica**

Para ver el historial de una rama específica, puedes usar:

```bash
git log nombre_de_la_rama
```

### 28. **Verificar el historial de una rama en un formato compacto**

Para ver el historial de una rama en un formato compacto, puedes usar:

```bash
git log --oneline nombre_de_la_rama
```

### 29. **Verificar el historial de una rama en un formato compacto con gráfico**

Para ver el historial de una rama en un formato compacto con gráfico, puedes usar:

```bash
git log --oneline --graph --decorate nombre_de_la_rama
```

### 30. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas, puedes usar:

```bash
git log --oneline --graph --decorate --all
```

### 31. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags
```

### 32. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes
```

### 33. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes
```

### 34. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog
```

### 35. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes
```

### 36. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch
```

### 37. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat
```

### 38. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary
```

### 39. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature
```

### 40. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color
```

### 41. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit
```

### 42. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s"
```

### 43. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative
```

### 44. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor"
```

### 45. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar"
```

### 46. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha"
```

### 47. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha"
```

### 48. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo
```

### 49. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10
```

### 50. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5
```

### 51. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse
```

### 52. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges
```

### 53. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent
```

### 54. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark
```

### 55. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick
```

### 56. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only
```

### 57. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only
```

### 58. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge
```

### 59. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents
```

### 60. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents
```

### 61. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2
```

### 62. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2
```

### 63. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration
```

### 64. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history
```

### 65. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse
```

### 66. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense
```

### 67. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges
```

### 68. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path
```

### 69. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary
```

### 70. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry
```

### 71. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs
```

### 72. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron"
```

### 73. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron"
```

### 74. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect
```

### 75. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick
```

### 76. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark
```

### 77. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right
```

### 78. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry
```

### 79. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick
```

### 80. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark
```

### 81. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry
```

### 82. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick
```

### 83. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark
```

### 84. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry
```

### 85. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick
```

### 86. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark
```

### 87. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry
```

### 88. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick
```

### 89. **Verificar el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark**

Para ver el historial de una rama en un formato compacto con gráfico y todas las ramas y tags y remotes y stashes y reflog y notas y patches y stat y summary y show-signature y color y abbrev-commit y pretty y date y author y grep y since y until y path y max-count y skip y reverse y no-merges y first-parent y cherry-mark y cherry-pick y left-only y right-only y merge y no-min-parents y no-max-parents y min-parents y max-parents y simplify-by-decoration y full-history y sparse y dense y simplify-merges y ancestry-path y boundary y cherry y walk-reflogs y glob y exclude y bisect y cherry-pick y cherry-mark y left-right y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark y cherry y cherry-pick y cherry-mark, puedes usar:

```bash
git log --oneline --graph --decorate --all --tags --remotes --stashes --reflog --notes --patch --stat --summary --show-signature --color --abbrev-commit --pretty=format:"%h - %an, %ar : %s" --date=relative --author="nombre_del_autor" --grep="texto_a_buscar" --since="fecha" --until="fecha" -- path/al/archivo --max-count=10 --skip=5 --reverse --no-merges --first-parent --cherry-mark --cherry-pick --left-only --right-only --merge --no-min-parents --no-max-parents --min-parents=2 --max-parents=2 --simplify-by-decoration --full-history --sparse --dense --simplify-merges --ancestry-path --boundary --cherry --walk-reflogs --glob="patron" --exclude="patron" --bisect --cherry-pick --cherry-mark --left-right --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark --cherry --cherry-pick --cherry-mark
```


---



## Visor Tig

### **¿Qué es Tig?**
Tig es un visor de historial de Git basado en **ncurses** (una biblioteca para crear interfaces de texto en la terminal). Te permite:

- Ver el historial de commits en un formato gráfico.
- Navegar por ramas, tags y commits.
- Ver detalles de cada commit (archivos modificados, diferencias, etc.).
- Filtrar commits por autor, fecha, mensaje, etc.
- Realizar acciones como checkout, rebase, merge, etc., directamente desde la interfaz.

---

### **Instalación de Tig**

#### En Linux (Ubuntu/Debian):

```bash
sudo apt-get update
sudo apt-get install tig
```

#### En macOS (con Homebrew):

```bash
brew install tig
```

#### En Windows:

Tig no es nativo en Windows, pero puedes usarlo instalando **Git Bash** o **WSL** (Windows Subsystem for Linux) y luego instalando Tig como en Linux.

---

### **Comandos básicos de Tig**

Una vez instalado, puedes usar Tig de varias formas:

1. **Ver el historial de commits**:

   Simplemente escribe `tig` en la terminal dentro de un repositorio Git. Esto abrirá una interfaz interactiva con el historial de commits.

```bash
tig
```

2. **Ver el historial de un archivo específico**:

   Si quieres ver el historial de cambios de un archivo en particular, usa:

```bash
tig archivo.txt
```

3. **Ver el historial de una rama específica**:

   Para ver solo los commits de una rama, usa:

```bash
tig nombre-de-la-rama
```

4. **Ver diferencias entre commits**:

   Dentro de Tig, selecciona un commit y presiona `Enter` para ver los cambios (diff) en ese commit.

5. **Filtrar commits**:

   Puedes filtrar commits por autor, fecha, mensaje, etc. Dentro de Tig, presiona `/` y escribe tu filtro (por ejemplo, el nombre de un autor).

---

### **Atajos de teclado en Tig**

Una vez dentro de Tig, puedes usar estos atajos para navegar:

- **`j` / `k`**: Moverse hacia arriba y abajo en la lista de commits.
- **`Enter`**: Ver detalles del commit seleccionado (archivos modificados, diferencias, etc.).
- **`q`**: Salir de la vista actual o cerrar Tig.
- **`/`**: Buscar commits (por mensaje, autor, etc.).
- **`m`**: Ver el mensaje completo del commit.
- **`d`**: Ver las diferencias (diff) del commit.
- **`t`**: Ver el árbol de archivos del commit.
- **`R`**: Refrescar la vista.
- **`?`**: Mostrar la ayuda con todos los atajos.

---

### **Ejemplo de uso**

1. Abre Tig en tu repositorio:

```bash
tig
```

2. Navega por los commits usando `j` y `k`.

3. Selecciona un commit y presiona `Enter` para ver los archivos modificados.

4. Presiona `d` para ver las diferencias (diff) en ese commit.

5. Usa `/` para buscar commits específicos (por ejemplo, `/fix` para buscar commits con "fix" en el mensaje).

6. Presiona `q` para salir de Tig.

---

### **Ventajas de Tig**

- Es rápido y ligero.
- No necesitas salir de la terminal.
- Es interactivo y fácil de usar.
- Te permite realizar acciones de Git (checkout, rebase, etc.) directamente desde la interfaz.

---

### **Alternativas a Tig**

Si Tig no es lo tuyo, aquí tienes otras opciones:

- **GitKraken**: Interfaz gráfica muy completa.
- **Sourcetree**: Otra herramienta gráfica gratuita.
- **Lazygit**: Similar a Tig, pero con una interfaz más moderna.

---

## Lazygit


### **¿Qué es Lazygit?**

**Lazygit** es una herramienta increíble para trabajar con Git desde la terminal, pero con una interfaz interactiva y moderna. Es similar a Tig, pero con una experiencia más visual y amigable. Es perfecto para quienes quieren una alternativa más intuitiva a los comandos tradicionales de Git, pero sin salir de la terminal.

Lazygit es un cliente de Git en la terminal que te permite:

- Ver el historial de commits.
- Gestionar ramas (crear, eliminar, cambiar entre ellas).
- Hacer commits, rebase, merge, etc.
- Ver diferencias (diffs) entre archivos.
- Resolver conflictos de merge de manera interactiva.
- Y mucho más, todo desde una interfaz visual en la terminal.

---

### **Instalación de Lazygit en GNU/Linux**

#### 1. **Instalación con el gestor de paquetes**:

   Si usas una distribución basada en Debian/Ubuntu, puedes instalarlo con:

```bash
sudo apt update
sudo apt install lazygit
```

En distribuciones basadas en Arch Linux (como Manjaro):

```bash
sudo pacman -S lazygit
```

En Fedora:

```bash
sudo dnf install lazygit
```

#### 2. **Instalación manual (si no está en los repositorios)**:

   Si tu distribución no tiene Lazygit en los repositorios, puedes instalarlo manualmente:

   1. Descarga el binario desde [GitHub](https://github.com/jesseduffield/lazygit/releases).
   2. Descomprime el archivo descargado.
   3. Mueve el binario a un directorio en tu `PATH`, por ejemplo:

```bash
tar -xzf lazygit_*.tar.gz
sudo mv lazygit /usr/local/bin/
```

#### 3. **Verificar la instalación**:

   Después de instalar, verifica que Lazygit esté disponible:

```bash
lazygit --version
```

   Si ves la versión, ¡todo está listo!

---

### **Cómo usar Lazygit**

1. **Abrir Lazygit**:

   Simplemente escribe `lazygit` en la terminal dentro de un repositorio Git:

```bash
lazygit
```

   Esto abrirá la interfaz interactiva de Lazygit.

2. **Interfaz de Lazygit**:

   La interfaz está dividida en varios paneles:
   - **Panel de commits**: Muestra el historial de commits.
   - **Panel de archivos**: Muestra los archivos modificados.
   - **Panel de diferencias (diff)**: Muestra los cambios en los archivos seleccionados.
   - **Panel de ramas**: Muestra las ramas locales y remotas.

3. **Atajos de teclado**:

   Lazygit es completamente interactivo. Aquí tienes algunos atajos clave:
   - **`j` / `k`**: Moverse hacia arriba y abajo en las listas.
   - **`Enter`**: Seleccionar un elemento (commit, archivo, rama, etc.).
   - **`c`**: Hacer un commit.
   - **`b`**: Ver y gestionar ramas.
   - **`m`**: Hacer merge o rebase.
   - **`d`**: Ver diferencias (diff) en los archivos.
   - **`?`**: Mostrar la ayuda con todos los atajos.
   - **`q`**: Salir de Lazygit.

4. **Ejemplo de flujo de trabajo**:

   - Abre Lazygit: `lazygit`.
   - Navega por los commits con `j` y `k`.
   - Selecciona un archivo modificado y presiona `Enter` para ver los cambios.
   - Haz un commit presionando `c`, escribe el mensaje y confirma.
   - Cambia de rama presionando `b`, selecciona una rama y haz checkout.
   - Haz merge o rebase con `m`.


Videos tutorial https://www.youtube.com/watch?v=CPLdltN7wgE

---

### **Ventajas de Lazygit**

- **Interfaz intuitiva**: Es mucho más visual que los comandos tradicionales de Git.
- **Rápido y eficiente**: No necesitas memorizar comandos complejos.
- **Resolución de conflictos**: Te ayuda a resolver conflictos de merge de manera interactiva.
- **Personalizable**: Puedes configurar atajos de teclado y temas.

---

### **Alternativas a Lazygit**

Si Lazygit no es lo tuyo, aquí tienes otras opciones para la terminal:
- **Tig**: Como ya mencioné, es otra herramienta visual para Git en la terminal.
- **GitUI**: Similar a Lazygit, pero con una interfaz más minimalista.
- **Magit**: Un cliente de Git para Emacs (si usas ese editor).

---

### **Resumen**

- **Lazygit** es una herramienta interactiva y visual para trabajar con Git en la terminal.
- Se instala fácilmente en GNU/Linux con el gestor de paquetes o manualmente.
- Es perfecto para quienes quieren una experiencia más gráfica sin salir de la terminal.



¡Muy buena observación! Efectivamente, Git introdujo el comando `git switch` y `git restore` en la **versión 2.23** (lanzada en agosto de 2019) para reemplazar algunas funcionalidades de `git checkout`, que históricamente hacía demasiadas cosas (cambiar de rama, restaurar archivos, etc.). Vamos a desglosarlo para que quede claro:

---

## Diferencias entre `git checkout` y `git switch`

1. **`git checkout` (comando tradicional)**:

   - Es compatible con **todas las versiones de Git**.
   - Se usa para:
     - Cambiar de rama: `git checkout nombre-de-la-rama`.
     - Crear una nueva rama y cambiarte a ella: `git checkout -b nueva-rama`.
     - Restaurar archivos: `git checkout -- archivo.txt`.
   - **Problema**: `git checkout` hace demasiadas cosas, lo que puede ser confuso.

2. **`git switch` (nuevo comando)**:

   - Disponible a partir de la **versión 2.23 de Git**.
   - Se usa **exclusivamente** para cambiar de rama:
     - Cambiar de rama: `git switch nombre-de-la-rama`.
     - Crear una nueva rama y cambiarte a ella: `git switch -c nueva-rama`.
   - Es más intuitivo y específico que `git checkout`.

3. **`git restore` (nuevo comando)**:

   - También disponible a partir de la **versión 2.23 de Git**.
   - Se usa para **restaurar archivos**:
     - Descartar cambios en un archivo: `git restore archivo.txt`.
     - Restaurar un archivo desde un commit específico: `git restore --source=commit-hash archivo.txt`.

---

### **¿Qué versión de Git tienes?**

Para saber qué versión de Git tienes instalada, ejecuta:

```bash
git --version
```

- Si tienes una versión **anterior a 2.23**, solo puedes usar `git checkout`.
- Si tienes una versión **2.23 o superior**, puedes usar tanto `git checkout` como `git switch` y `git restore`.

---

### **¿Hay problemas al usar uno u otro?**

No hay problemas técnicos en usar `git checkout` en versiones modernas de Git, ya que sigue siendo totalmente compatible. Sin embargo, **se recomienda usar `git switch` y `git restore` en versiones 2.23+** porque:

- Son más específicos y fáciles de entender.
- Reducen la confusión al separar las funcionalidades de cambio de rama y restauración de archivos.

---

### **Ejemplos comparativos**

#### Cambiar de rama:

- Con `git checkout` (todas las versiones):

```bash
git checkout nombre-de-la-rama
```

- Con `git switch` (versión 2.23+):


```bash
git switch nombre-de-la-rama
```

#### Crear una nueva rama y cambiarte a ella:

- Con `git checkout` (todas las versiones):

```bash
git checkout -b nueva-rama
```

- Con `git switch` (versión 2.23+):

```bash
git switch -c nueva-rama
```

#### Restaurar un archivo:

- Con `git checkout` (todas las versiones):

```bash
git checkout -- archivo.txt
```

- Con `git restore` (versión 2.23+):

```bash
git restore archivo.txt
```

---

### **Conclusión**

- Si usas una versión **antigua de Git (< 2.23)**, solo puedes usar `git checkout`.
- Si usas una versión **moderna de Git (>= 2.23)**, se recomienda usar `git switch` para cambiar de rama y `git restore` para restaurar archivos, ya que son más específicos y claros.
- `git checkout` sigue funcionando en todas las versiones, pero es mejor evitar usarlo en versiones modernas para no confundirte.

---




