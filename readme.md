# Git and GitHub

En este repositorio podremos observar pruebas asociadas con Git y GitHub.
Es por ello que es un proyecto meramente de aprendizaje.
Es importante destacar que este README.md sigue en construcción.

## Comandos iniciales

- git init: para crear el repositorio (.git)
- git status: para ver el estado de lo comiteado
- Para obtener información sobre un comando git, por ejemplo, git checkout:
  - Resumido en terminal: git checkout -h
  - Desarrollado en otra pestaña: git checkout --help
- git log: para ver mis commits y los hash asociados a ellos.
- git add .: para añadir a la staging area commits que renombraremos con;
- git commit -m "Nombre del commit en ingles y con la primera letra en mayúscula".

Hay tres tipo de commits: blob, tree y commit:
- git cat-file -t dd256: -t te dice el TIPO de commit que es.
- git cat-file -p dd256: -p te dice LO QUE CONTIENE dentro que puede ser un commit de tipo tree, commit o blob.
*Con los 5 primeros caracteres como mínimo, y si no esta repetido, números y letras de a hasta f. Summa del nombre de la carpeta que se crea en objects (2caracteres) junto con los el nombre del archivo creado (3 caracteres)*

Git organiza tu historial utilizando tres componentes clave en su sistema de almacenamiento. La diferencia principal radica en su función: el blob almacena el contenido de los archivos, el tree organiza estos elementos en carpetas, y el commit sella el estado del proyecto en el tiempo.
1. Blob (Binary Large Object)
Qué es: Es la unidad básica de almacenamiento de Git. Contiene únicamente el contenido en bruto del archivo.*Características*: No almacena metadatos, nombres de archivo ni estructura de carpetas. Si tienes el mismo texto exacto en 10 archivos diferentes, Git solo creará un blob y lo reutilizará para ahorrar espacio.
2. Tree (Árbol)
Qué es: Representa la estructura de directorios (carpetas) de tu proyecto.
*Características*: Esencialmente es una lista que vincula los hashes de los blobs (tus archivos) con sus metadatos: nombres, permisos y ubicación. Un tree puede contener a su vez otros trees (para sub-carpetas) y blobs (para archivos).
3. Commit (Confirmación)
Qué es: Es una instantánea (snapshot) de todo el proyecto en un momento específico.
*Características*: No almacena los archivos directamente, sino que apunta a un único tree (el directorio raíz del proyecto en ese momento). Además, contiene metadatos vitales: el autor, la fecha, el mensaje del commit y los hashes de sus commits anteriores (padres) para formar el historial.

Hay que tener en cuenta que cuando actualizamos un commit se crea un nuevo hash que será el padre del creado inicialmente para ese archivo o carpeta. A su vez puede crear otro hash para el archivo cambiado  ya que al actualizarse  ya no tendrá el mismo hash. Sin embargo, dentro de este nuevo nuevo commit y hashes, mantendrá el hash de un archivo que no se ha modificado.

El nuevo commit apuntará como padre al anterior commit inicial. Las referencias padres nos sirven para saber desde dónde vienen los nuevos creados.

- git show: Muestra los cambios de un commit
- git clone: Clona un repositorio de Git

## Comandos asociados a restauración de commits y modificación de ramas

- Git reset: modifica el historial de commits(altera el pasado). No toca el HEAD. Modifica el puntero de la RAMA. "No me gustan los dos nuevos commits que he hecho y me voy al commit Patata5 que hice , me olvido de Patatín6 y Potato7, con los que continué, y el garage collector los borrará pasado un tiempo."

*Funcionamiento*: 
Git reset HEAD~3 te conduce hasta tres commits para atrás y los deja en la working área. 
Git reset HEAD~3 --hard te lleva tres commits hacia atrás y los tres commits anteriores se han quedado huérfanos y en poco tiempo se borrarán. 
Git reset <5 primeros caracteres al que quiero volver (aunque se haya quedado huérfano con el reset anterior)> --hard: vuelve al commit que le indicas (la garbage collector no borra hasta en unas semanas después).
Git reset <hash commit (5 primeros caracteres mínimo)> --soft te deshace el commit hecho, te lleva a ese commit y te lo deja en la working area, por tanto puedes modificar el título o el contenido en tu zona de trabajo (es como darle a deshacer el último commit a través de VSC).
Git reset es muy útil cuando trabajamos individualmente o en local.

- Git commit --amend: hace lo mismo que reset pero ya sabe que es con el último commit. Típico para cambiar el título del último commit. Rehace el último commit (contenido también) y el anterior queda huérfano.

- git restore: creado a partir de git checkout, realiza todas las operaciones de checkout NO relativas a ramas. Restaura lo anterior?
- git switch: creado a partir de git checkout, realiza todas las operaciones de checkout relativas a ramas. No se usa, se sigue usando git checkout.

### Ramas (branches)

Comandos para trabajar con ramas

- `git branch`: Lista las ramas locales
- `git branch nombre_rama`: Crea una nueva rama
- `git checkout nombre_rama`: Cambia a la rama especificada
-  git checkout: cambia el puntero HEAD (o ) para explorar commits o restaurar archivos sin borrar la historia. Movemos el puntero HEAD y permite manejar las ramas, por lo que no dejamos commits huérfanos, no se ha destruido nada.
- `git checkout -b nombre_rama`: Crea una nueva rama y cambia a ella (-b de branch 🥲)
- `git merge nombre_rama`: Fusiona la rama especificada con la rama actual

- branches
  - Crear, borrar, intercambiar
  - Crear desde ref (git checkout b mybranch master~1)

  - git push -u origin <nombre de la rama ya creada en local>: publicaremos la rama Patatillas creada recientemente. Las ramas nuevas no se publican al haberlo hecho ya con la inicial (MAIN).

  - git remote: genera el enlace del remoto de nuestro origin (por ejemplo podemos querer una rama en GitLab y no en GitHub).

  - git merge: 
      -> git merge: por defecto actualiza la rama con los nuevo commits. A esto se le llama Fast fordward. 
      -> git merge --no-ff Patatillas: en el caso de que haya bifurcación real (MAIN ha continuado creciendo por un lado y Patatillas también pero por otro lado) para que no se pierda ninguno de esos commits bifurcados, crea un commit recogiendo, reconciliando y agrupando a los dos hijos. Puede usarse git merge también peeeero  no se quedarán especificado de dónde vienen los dos hijos concretamente, por lo que es preferible usar git merge --no-ff Patatillas

  - git push -f. Por ejemplo:
          1. Subimos un commit a GitHub
          2. Lo hemos modificado en nuestro local borrando el último titulo del commit pusheado a GitHub.
          3. Tenemos en local una cosa y en GitHub otra.
          4. Forzamos que suba lo que tenemos en local a GitHub con git push -f porque estamos seguros de que queremos que lo actualice.

## PULL REQUEST

Sirven para informar a nuestro equipo sobre en qué estamos invirtiendo nuestro trabajo. 
Podremos interaccionar con el equipo en ellas para que se revisen las pull request. 
El enfoque es compartir la información entre el equipo.


## DETALLES

- HEAD no apunta a los commits sino a las ramas: main (principal), feature (secundarias). Pueden apuntar a commits directamente pero no es recomendable. Hay que tener en cuenta que HEAD siempre apuntará al commit activo ya sea a través de una referencia commit o rama.

- Si el puntero de mi MAIN apunta a un commit anterior tengamos en cuenta que volveremos a ver el commit sin las actualizaciones a archivos o carpetas realizadas.

- Los logs guardan los commits creados, aunque hayan sido borrados o reseteados, por eso, con ellos, podemos ver los commits huérfanos. Ten en cuenta que los commits huérfanos no subidos a GitHub solo estarán en local. Puedes ver los logs con git reflog o con GIT GRAPH en opciones añadimos la pestaña "Include commits only mentioned by rellogs".

- Las ramas son etiquetas que puede apuntar a una cadena de commits o a una bifurcación. Al borrar una etiqueta no borras los commits, solo debes volver a crearla y asociarla a esos commits con "git branch <nombre de la nueva rama Patatillas> <hash commit (5 primeros caracteres mínimo)>". En este caso hay que tener en cuenta en qué etiqueta nos encontramos, si estamos en MAIN y creamos la nueva rama Patatillas apuntando al nuevo commit formado cuando estamos en MAIN, hay que recordar que ambas etiquetas, MAIN y Patatillas, apuntan a ese commit. 
Por tanto, además del comando git branch habría que realizar un git reset situados en MAIN hacia el commit que queremos que apunte.
Por último, haremos git checkout hacia la nueva rama creada Patatillas para seguir trabajando desde ahí, que era lo que pretendíamos.

Evidentemente, es más organizado, crear la rama Patatillas antes de crear el commit desde otra rama MAIN. Así, solo tendremos que hacer git checkout -b <nombre de la rama> para crear la rama y cambiar a ella para continuar con los commit que queramos añadir a esta nueva etiqueta.