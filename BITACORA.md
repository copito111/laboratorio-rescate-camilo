# Bitácora del laboratorio de rescate.

## Reto 1. Ver el historial

**¿Qué muestra cada comando?**

- `git log` muestra los commits con su identificador completo, autor, fecha y mensaje.
- `git log --oneline` resume cada commit en una línea con su identificador abreviado y el título del mensaje.
- `git log --oneline --graph --all` muestra un dibujo en texto de cómo se conectan los commits de todas las ramas y demás referencias.

**¿Qué es el código que aparece al inicio de cada commit?**

Es el hash que identifica ese commit. Git muestra una versión corta con `--oneline`, y puedo usarla para referirme a ese commit si es única en el repositorio.

## Reto 2. Ver qué cambió antes de guardar

**¿Por qué el segundo `git diff` no mostró nada?**

Porque usé `git add notas.txt` y el cambio pasó al área de preparación. `git diff` muestra los cambios que todavía están fuera de esa área.

**¿Qué muestra `git diff --staged`?**

Muestra los cambios preparados para el próximo commit, comparados con el último commit.

## Reto 3. Recuperar un archivo borrado

**¿Qué hace `git restore notas.txt`?**

Recupera `notas.txt` en mi carpeta de trabajo usando la versión que Git tiene en el área de preparación. En este ejercicio esa versión coincide con la del último commit.

**¿Funcionaría si nunca hubiera hecho commit del archivo?**

Si el archivo nunca se agregó con `git add` ni se guardó en un commit, Git no tiene una copia para recuperarlo. Si ya estaba en el área de preparación, sí puede restaurarlo desde allí aunque todavía no haya un commit de ese archivo.

## Reto 4. Sacar un archivo del área de preparación

**¿Qué diferencia hay entre `git restore` y `git restore --staged`?**

`git restore archivo` restaura el contenido del archivo en mi carpeta de trabajo y puede descartar cambios sin preparar. `git restore --staged secreto.env` saca el archivo del próximo commit y conserva su contenido en mi carpeta.

## Reto 5. Corregir el mensaje de un commit

`git commit --amend -m "docs: agrega línea 4 a notas"` reemplaza el último commit. En este ejercicio conservé el cambio de `notas.txt` y corregí el mensaje. Lo hice antes del `push` porque ese comando reescribe el commit y cambia su hash.

## Reto 6. Deshacer un commit que ya subí

**¿`git revert` borró el commit equivocado o creó uno nuevo?**

Creó un commit nuevo que deshizo los cambios de `fix: limpia notas`. El commit original quedó en el historial y la línea 4 de `notas.txt` volvió a su versión anterior.

**¿Por qué es la opción segura cuando ya se hizo `push`?**

Porque conserva el historial que ya se compartió en GitHub. Puedo subir el commit de reversión con un `git push` normal.

## Reto 7. Deshacer un commit local y conservar sus cambios

**¿Qué diferencia hay entre `git reset --soft` y `git revert`?**

`git reset --soft HEAD~1` mueve la rama al commit anterior y deja los cambios del último commit preparados. `git revert` crea un commit nuevo que deshace los cambios del original y lo conserva en el historial.

**¿Cuándo se usa cada uno?**

Uso `git reset --soft` si todavía no he subido el commit y quiero conservar los cambios para completarlos. Uso `git revert` si el commit ya está compartido y quiero deshacerlo sin reescribir el historial.

## Reto 8. Guardar temporalmente el trabajo a medias

**¿Para qué sirve `git stash`?**

Sirve para guardar temporalmente los cambios que tengo en archivos que Git ya rastrea. Así puedo cambiar de tarea sin hacer un commit del trabajo incompleto.

**¿Qué hace `git stash pop`?**

Recupera los cambios que guardé más recientemente con `git stash`. Si se aplican correctamente, los quita de la lista de cambios guardados.

## Punto 9. Historial al cierre del laboratorio

Resultado de `git log --oneline --graph` antes del commit de la bitácora.


```text
* b083bd9 docs: agrega línea 5 a notas
* 351e541 feat: agrega borrador completo
* a738ad0 Revert "fix: limpia notas"
* 1bee64b fix: limpia notas
* 4590f56 docs: agrega línea 4 a notas
* c1a5fa2 chore: agrega .gitignore para archivos .env
* 730a003 feat: agrega notas y bitacora
* 84c0439 Initial commit
```
