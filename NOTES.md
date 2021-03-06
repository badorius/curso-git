# CURSO GIT MASTERMMIND
```bash
git config --global user.email "badorius@gmail.com" 
git config --global user.name "badorius" 
git version
git init ->crear repo git
git status -> ver que ficheros gestiona git
git add index index.html -> lo pasamos a stageing area, faltara el commit
git status -> para ver index.html en stageing
git commit -m " add index.html" 
```

##### Modificamos el index.htm
```bash
git status -> veremos que hemos modificado el index.html (tambien lo veremos en el editor)
git add index.html
git commit -m "Aadido el contenido del blog" 
git log -> vemos los dos commits realizados y el que esta activo en el master
git checkout f1daaa3256fff3d246f1a3528ac583309c3fbd33 -> para volver a la version anterior (cogiengo el hash de git log) nos muestra un warging de deatached HEAD
git checkout b69178081f1f594e4603c52b47d31a10ac2d8f4a -> volvemos a la ultima, veremos que el texto en el editor se nos actualiza
git checkout master -> esto nos devuelve al ultimo commit que hemos realizado y dejamos de estar de deatached HEAD. Mas adelante veremos las ramas.
```

##### Como deshacer cambios, no me gusta el ultimo cambio y buscamos una manera mejor de haccerlo
```bash
git reset f1daaa -> eliminamos el commit que no queremos, lo revisamos con un git log
git log
git add index.html
git status -> veremos que el index.html ha estado modificado.
git commit -m "Contenido del blog"  -> hacemos el commit con el nuevo cambio 
git log -> lo verificamos
git reset --hard f1daaa -> A diferencia del anterior, este lo elimina de manera definitva todos los cambios del hash en adelante, es cuando lo realizado ya no se quiere.
```
##### Recreamos el index.html con el contenido correcto y luego

```bash
git add index.html
git commit -m " Contenido del blog" 
git log --oneline -> para que lo muestre en una sola linea
```

##### Borramos por error un fichero gestionado con el git (rm index.html) no perdemos nada si no hacemos git reset --hard
```bash
git status -> veremos que hemos eliminado el index.html
git restore index.html-> restauramos el fichero index.html
```
##### Todos los archivos y carpetas estan en la carpeta .git

##### Aadimos mas ficheros, populamos el fichero style.css y hacemos cambios en el index.html i la img
```bash
git add . -> metemos todo el directorio actual en stageing area
git commit -m "Create Navbar"
```
##### Subir contenido en github (se puede subir por ssh o https)
```bash
git remote add origin git@github.com:badorius/curso-git.git
git remote -v -> de donde podemos descargar (fetch) o subir (push)
git branch -M main -> cambiar el nombre de la rama, por ahora lo dejaremos como master
```

##### Crear claves ssh antes de hacer el push
```bash
ssh-keygen -t ed25519 -C "pepito@gmail.com" (generamos clave publica y privada) en setings de github, subimos la pub
git push -u origin master -> esto solo la primera vez, las siguientes git push 
```
##### Como crear ramas, si hay varias personas trabajando en el mismo proyecto, no es buena idea trabajar en la rama principal (master) creamos una bifurcaci??n en la rama principal (master o main) 
##### Cada uno trabaja en una rama y al final se mezclan las ramas en el master, es mas facil para solucionar conflictos.

```bash
git checkout -b feature-posts-styles -> Al igual que antes utiliz??bamos el checkout para volver a un commit anterior, ahora lo utilizaremos para crear una nueva rama
git branch -> veremos en que rama estamos, en el editor tambi??n en la barra inferior.
```

##### Realizamos cambios en el index.html y sytle.css, una vez realizados los cambios, al estar en la rama feature-posts-styles
```bash
git status -> revisamos los cambios
git add index.html
git commit -m "Add post html"
git add style.css
git commit -m "Add post style"
```
##### Podriamos a??adir los dos ficheros a la vez y realizar un ??nico commit, pero de esta forma lo hacemos m??s granular.
##### Aqu?? hemos finalizado la rama, ahora hay que a??adir nuestra rama al master
```bash
git log --oneline
```
##### Ahora hemos creado una rama en local, pero hay que crearla en github, con esto creamos y subimos la nueva rama
```bash
git push -u origin feature-posts-styles
```
##### Tanto en github como en el vscode podremos ver la nueva rama todos los cambios, si cambiamos a la rama master no veremos los cambios de la nueva rama
```bash
git checkout master ->cambiamos a master y no vemos los cambios de la rama feautre-posts-estyles
git checkout feature-posts-styles -> cambiamos de nuevo a la rama feature-posts-styles
```

##### En git hub ya nos muestra una alarma de que existe una rama con la opci??n de compare & pull request.
##### Ahora realizaremos otro clone, para simular otra persona trabajando en otra rama. La ruta la copiamos del bot??n code->ssh de github
```bash
git clone git@github.com:badorius/curso-git.git persona-backend
```
##### Volvemos a la rama master y creamos un README.md Antes hacemos los add, commit y push
```bash
git add notes.txt 
git status
git commit -m "Add post notes.v3"
git push -u origin feature-posts-styles
git checkout master
```
##### Creamos un fichero READM.md y lo populamos, (sintaxis markdown) hacemos add, commit y push, podemos ver el readme en el git. Ahora tenemos modificaciones diferentes en las dos ramas, hasta que no las mezclemos.
##### Para hacer el merge en github click con compare & pull request le damos un t??tulo y creamos el pull request. confirmamos el cambio 
```bash
git checkout master
git pull -> hemos descargado los cambios merged en local.
```
##### Mezclar rams en local
##### Cada vez se nos asigna una tarea, normalmente crearemos una rama nueva y luego haremos el merge.
```bash
git checkout -b feature-adds
```
##### Modificamos el html
```bash
git add .
git commit -m "Add advertisment html"
```
##### Ahora nos damos cuenta que esta nueva rama, ser?? muy complicada y tendremos muchos commits, hacemos una nueva rama dentro de esta ultima

```bash
git checkout -b feature-load-adds-from-api
```
##### Creamos el index.js y hacemos el commit
```bash
git add .
git commit -m "Create load adds function"
```
##### Estas ramas solo existen en local, no estan en el gi, a no ser que hagamos un push -u origin $NOMBRE_RAMA
##### Mezclamos la rama de publicidad y su subrama en local, volvemos a la rama anterior con
```bash
git checkout feature-adds
```

##### Una vez en la rama feauture-adds, meclamos la rama en la que estamos con la anterior con feature-load-adds-from-api
```bash
git merge feature-load-adds-from-api
```
##### Ahora mezclamos todo en github
##### Lo podemos subir/crear la rama feature-adds en github y luego hacer el merge en master
```bash
git push -u origin feature-adds
```
##### O podriamos pasar en local a master, hacer el merge y luego hacer un push del master
```bash
git checkout master
git merge feature-adds
git log --oneline
git log --graph --oneline #vemos los logs de las ramas/tareas
```

##### Un ejemplo, te dan una tarea de backend y  frontend, creas una rama de master de backend y en local creas unasubrama de frontend
##### en loccal vas trabajando en una rama, vas cambiando y luego trabajas en otra y cuando las tienes completadas, haces un merge del backend y frontend
##### y solo haces un push de una rama para luego hacer un unico merge en el master de tu tarea frontend/backend.

##### Como hacer un fork y a??adir cambios
##### Se puede contribuir a un proyecto open source, descargar un proyecto
##### se hace un fork de un repositorio a tu git hub, subir los cambios a tu github y cuando este listo, hacer un merge de tu github a otro repositorio.
##### Simularemos un forkk con el mismo git de cursogit
##### Vamos a github https://github.com/mastermindac/curso-git, proyecto curso-git y le damos a fork, seleccionamos nuestra cuenta.
##### como hacemos cambios en este fork, copiamos el enlace ssh y hacemos un git clone 
##### vamos al index.js y ponemos un comentario //video pull request
```bash
git clone git@github.com:badorius/curso-git-1.git
```
##### Hacemos la modificacion en el index.js y creamos una rama
```bash
git checkout -b feature-video-pull-request
git add .
git commit -m "Video pull requesst"
```

##### Lo subimos, pero hay que crear la rama en remoto
##### Si te clonas un repositorio, tiene ya el origin predefinido, lo podemos ver con git remote -v
##### Como ya tenemos el origin, lo subimos al origin
```bash
git push -u origin feature-video-pull-request 
```
##### Ahora en github nos vamos a contribute open pull request, ah?? seleccionamos el origen destino, en este caso orgine nuestra rama que haremos merge a la master de mastermindac
##### En entornos profesionales, normalmente la rama master es el codigo que hay en producci??n la que hay en los servidores, luego puede existir, la dev, test, etc.c..

##### Como resolver conflictos
##### Con un supuesto bug, vamos a issues y creamos un issue Titulo bug... comentarios...
##### Para resolver el bug, primero siempre un pull para actualizar todos los cambios
```bash
git pull
git checkout -b bugfix-2-curso-git -> el numero 2 corresponde al ide de issue en github
```
##### Que pasa si otra persona al mismo tiempo decide arreglar este bug.
```bash
git clone git@github.com:badorius/curso-git.git persona2-curso-git
git checkout -b bugfix-2-curso-git-persona2
```
##### Ahora tanto persona 1 como persona 2 suben los cambios
##### Persona 1
```bash
git add .
git commit -m "Fix #2"
git push -u origin bugfix-2-curso-git
```

##### persona 2
```bash
git add .
git commit -m "Fix #2 persona2"
git push -u origin bugfix-2-curso-git-persona2
```

##### Ahora vamos github y vemos varias ramas, su historial partio del mismo commit, pero tienen conflictos en los cambios
##### Mezclaremos la primera rama, seleccionamos la rama,  pull request y merge.
##### Hacemos lo mismo con la rama de la persona2 y nos muestra un error de que no se puede hacer merge
##### Para ver los conflictos, hacemos el  pull request y le damos a resolve conflicts, nos muestra un editor donde nos mostrar?? el conflicto y podemos rectificar/ver
##### Si es algo simple se puede hacer desde github, pero normalmente se puede hacer desde vscode. para hacerlo desde el vscode,
##### Nos vamos al git de la persona 1 y hacemos un pull para descargar la ultima version con el bugfix de la persona 1
```bash
git pull
```
##### Cambiamos a la rama de la persona dos
```bash
git checkout master
git config pull.rebase false 
git pull origin bugfix-2-curso-git-persona2
```
##### En vscode aceptamos o modificamos la version que queremos e incluso podemos a??adir algo
```bash
git add index.jsgit commit -m "
```

##### Rebase interactivo
```bash
git checkout -b feature-affiliate-links -> subiremos esta rama con un ??nico pull request
git branch front -> internamente trabajaremos en dos ramas
git branch back
git checkout back
```
##### Editamos indejx.js
```bash
git add .
git commit -m "Cambio backend 1"
```
##### Editamos index.js cambio 2
```bash
--->>
git commit -a -m "Cambio backend 2" --->> con -a hacemos un add y un commit a la vez
--->>
```
##### Hacemos lo mismo cambio 3 para tener m??s comits, editamos el index.js

```bash
git commit -a -m "Cambio backend 3" 
```
##### Ahora pasamos al front 
```bash
git checkout front
```
##### Modificamos el index.html y hacemos -a commit/s
```bash
git commit -a -m "Cambio front 1"
```
##### Verificamos los cambios
```bash
git log -n 3 --oneline
```
##### Tenemos los cambios del back y del front, tenemos que juntarlos y luego hacer un pullrequest
##### Solo queremos un commit para cada cosa, back/front
```bash
git branch -> Vemos las ramas del repositorio
```
##### Dentro de front mezclamos la rama de back
```bash
git merge back
git log -n 7 --oneline
```
##### Ahora limpiaremos los commits antes de hacer el push para limpiar el historial
##### Dentro de front despues del merge 
```bash
git rebase -i feature-affiliate-links -> el rebase nos aplasta la rama hasta la que estemos, al ser interactivo -i nos abre el vim, cambiaremos de pick a squash  para que solo quede un front y un back
```
##### Luego guardamos los squash/pich y nos abre el fichero para modificar los mensajes, borramos los mensajes cambios frontend 1/2/3 a cambios frontend
```bash
pick 7c05e02 Cambio frontend1
squash 6afc01c Cambio frontend 2
squash e366146 Cambio notes 2
pick cb4fa06 Cambio backend 1
squash 86310d2 Cambio backend 2
squash b93c8d3 Cambio backend 3
squash 63c2b55 Cambio notes 4

Cambio frontend
```

##### Ahora lo revisamos con git log --oneline -n 6
##### Ahora lo pasamos a la rama de afiliados
##### En el minuto 06:34, si hicieramos el rebase estando en feature-affiliate-links y trayendo front, no har??a falta hacer el merge del final. Es decir:
```bash
git checkout feature-affiliate-links
git rebase -i front
git merge front
git branch -D front back
git push -u origin feature-affiliate-links
```

##### Ahora en github hacemos el pull request, veremos que solo tiene 2 commits
##### El rebase solo se recomienda hacer en local, nunca en github ya que generariamos un conflico con el trabajo de otras personas.

##### Squase and merge
```bash
git checkout master
git pull
git checkout -b feature-videos
```
##### Hacemo cambios en index.js
```bash
git commit -a -m "Cambios videos 1"
git commit -a -m "Cambios videos 2"
```
##### Ahora nos equivocamos con el titulo del commit y lo queremos modificar
```bash
git commit -a -m "Cambios videos 2"
git commit --amend -m "Cambios videos 3" --> Con esto cambiaremos el ??ltimo titulosiempre que no este subido a github
```
##### Ahora subimos a github
```bash
git push -u origin feature-videos
```
##### Ahora vamos a guithub para crear el pullrequest, hacemos pullrequest dentro de la rama y despu??s en el bot??n de merge, desplegamos y teenemos varias opciones
##### Rebase que ser??a la misma que hemos visto en eel capitulo anterior, podemos elegir distintos commits
##### Si hacemos un squash, nos los mezclaria todos los commits que tenga esta rama
##### Si hacemos cambios en un archivo y luego vemos que los queremos descart, dejar como el original, no hace falta hacer un commit y luego un reset para eliminarlos, podemos hacer un
```bash
git restore index.js -> Pone el archivo como estaba en el ultimo commit.
```

#####STASH
```bash
git checkout feature-affiliate-links
```
##### Hacemos cambios en index.html en algun momento alguien pone un bug issue en afiliados mientras tu estas trabajando. contrl k c (comand comment) <!-- cambio 3 --> 
##### Vamos a github i ponemos un issue en afiliates, titulo bug affiliate, en etiquetas podemos poner que es un bug, as?? saldr?? etiquetada como bug, creamosel issue
##### Una vez abierto el issue, que opciones tenemos:
##### Podemos aplicar los czmbios que estamos haciendo y hacer un commit en la rama que estamos y abrir una nueva rama para resolver el issue y luego subirlo.
##### Otra opci??n es el stash, m??s sencillo, deshacemos los cambios realizados, pero no los perdemos, quedan almacenados, no son commits ni stage area,se pueden recuperar en cualquier momento.
##### Si hacemos un 
```bash
git stash -> desaparecen los cambios del index.html
```
##### Ahora arreglamos el bug, a??adiendo una funcion de afiliados en el index.js, hacemos un commit
```bash
git add .
git commit -m "Fix affiliate links bug #7"
git push -u origin feature-affiliate-links
```

##### Ahora hay que hacer un pullrequest/merge y cerrar el issue
##### Ahora para recuperar los cambios en esta misma rama
```bash
git stash list (WIP= work in progress, no lo mezcles a??n, pero puedes darle un vistazo)
git stash pop -> veremos que recuperamos las entradas que ten??amos en el index.html, luego ya podemos hacer un add commit push
git add .
git commit -m "Cambios afiliados"
git push 
```

##### Tag y versionado sem??ntico. con git tag hacemos versiones de la aplicaci??n ex. 1.4.5
##### Si buscamos en google versionado sem??ntico, hay tres n??meros ejemplo 2.0.0 
##### Versi??n mayor Si hacemos un cambio que tiene un impacto o modifica la API / funciones, hay funciones que dejaran de funcionar, lo que cambiariamos a 3.0.0
##### Versi??n menor, cuando hacemos un cambio que es compatible con versiones anteriores, haces un cambio en la librer??a que a??ade una funci??n nueva, pero mantenemos compatibilidad, pasar??amos a 2.1.0
##### Si arreglamos un bug pasar??amos a la 2.0.1
##### Para hacer esto en git, lo hacemos con git tag, para asociarlo a un commit especificio:
```bash
git tag -a v0.1.0 -m "Primera versi??n del curso de Git de Mastermind"-> El primer n??mero si est?? en 0 est?? en desarrollo, la que tiene el 1 ya ser??a la que est?? en producci??n.
git tag -> Vemos listado de todos los tags
git show v0.1.0 -> nos muestra info del tag.
git push origin v0.1.0 -> Subimos el tag
```
##### Hacemos modificaciones en el codigo para producci??n ready y modificamos la versi??n.
##### Modificamos el fichero y hacemos
```bash
git add .
git commit -m "Producction ready"
git push
```
##### Ahora nos iremos a github y hacemos lo mismo desde github -> Create a new release -> Chose tag
##### Version 1.0.0 versi??n prod descripci??n - > publish, ahora tenemos dos releases.

##### Usa markdown para renderizar c??digo
##### Creamos un issue en alg??n repositorio porque has tenido un error con una librer??a,
##### Problema en la funci??n get comments, en el texto descriptivo queremos indicar la funci??n que nos da error, el c??digo y la salida del error:

```bash
Esta es la funci??n que me da error
```javascript
const getCommentsForEachPost = async (posts) => {
  const res = await Promise.all(posts.map(post => 
    fetch(`${url}/comments?postId=${post.id}&_limit=5`)
  ));
  console.log(res); 
  const postComments = await Promise.all(res.map(r => r.json()));
  
  postComments.forEach((comments, i) => posts[i].comments = comments);
}
```

Este es el error que muestra:
```bash
error: unknown switch `l'
usage: git commit [<options>] [--] <pathspec>...

    -q, --quiet           suppress summary after successful commit
    -v, --verbose         show diff in commit message template

Commit message options
    -F, --file <file>     read message from file
    --author <author>     override author for commit
    --date <date>         override date for commit
    -m, --message <message>
                          commit message
    -c, --reedit-message <commit>
                          reuse and edit message from specified commit
    -C, --reuse-message <commit>
                          reuse message from specified commit
    --fixup [(amend|reword):]commit
                          use autosquash formatted message to fixup or amend/reword specified commit
    --squash <commit>     use autosquash formatted message to squash specified commit
    --reset-author        the commit is authored by me now (used with -C/-c/--amend)
    --trailer <trailer>   add custom trailer(s)
    -s, --signoff         add a Signed-off-by trailer
    -t, --template <file>
                          use specified template file
    -e, --edit            force edit of commit
    --cleanup <mode>      how to strip spaces and #comments from message
    --status              include status in commit message template
    -S, --gpg-sign[=<key-id>]
                          GPG sign commit

Commit contents options
    -a, --all             commit all changed files
    -i, --include         add specified files to index for commit
    --interactive         interactively add files
    -p, --patch           interactively add changes
    -o, --only            commit only specified files
    -n, --no-verify       bypass pre-commit and commit-msg hooks
    --dry-run             show what would be committed
    --short               show status concisely
    --branch              show branch information
    --ahead-behind        compute full ahead/behind values
    --porcelain           machine-readable output
    --long                show status in long format (default)
    -z, --null            terminate entries with NUL
    --amend               amend previous commit
    --no-post-rewrite     bypass post-rewrite hook
    -u, --untracked-files[=<mode>]
                          show untracked files, optional modes: all, normal, no. (Default: all)
    --pathspec-from-file <file>
                          read pathspec from file
    --pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character
    ```
    ```
