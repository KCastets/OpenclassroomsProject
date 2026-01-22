# Projet de prise en main de Git

Il s'agit d'un projet fictif de site internet pour prendre en main Git et GitHub.
Dans ce ReadMe, il y aura les commandes suivies pas à pas pour : 
- Initialiser l'envirronement de travail Git en local
- Initialiser le dépot Git
- Suivre le cycle de vie du développement du projet fictif.

## Initialisation de l'environnement de travail

Pour initialiser l'environnement de travail, il y a quelques informations à renseigner (username, mail).
Il est possible d'apporter quelques configurations notamment quand à la colorisation des messages Git.

~~~ bash
$ git config --global user.name "KCastets"
$ git config --global user.email "killiancastets@gmail.com"
$ git config --global color.diff auto
$ git config --global color.status auto
$ git config --global color.branch auto
$ git config --global core.editor vim
$ git config --global merge.tool vimdiff

# Pour vérifier que nos configurations sont prises en compte : 
$ git config --list

user.name=KCastets
user.email=killiancastets@gmail.com
color.diff=auto
color.status=auto
color.branch=auto
core.editor=vim
merge.tool=vimdiff
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
~~~

## Initialisation du dépot Git

Pour initialiser un dépot Git, il faut d'abord créer un dossier :

~~~ bash
$ mkdir FirstProject
~~~

La commande 'git init' va initialiser le dépot git en créant les fichiers nécessaires :

~~~ bash
$ cd FirstProject
$ git init
$ ls -la

drwxr-xr-x 3 kcastets kcastets 4096 Jan 22 10:15 .
drwxr-xr-x 3 kcastets kcastets 4096 Jan 22 09:41 ..
drwxr-xr-x 7 kcastets kcastets 4096 Jan 22 10:14 .git
~~~

## Cycle de développement

Nous pouvons commencer à créer notre site internet.
Pour cela, nous créons un premier fichier index.html:

~~~ bash
$ touch index.html
~~~

En faisant la commande : 
~~~ bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ReadME.md
        index.html

nothing added to commit but untracked files present (use "git add" to track)
~~~

On voit que :
- Il n'y a pas de commit
- Nos fichiers sont 'untracked', c'est à dire qu'ils ne sont pas encore indexés (Zone 'Stage': Le fichier existe mais n'appartient mais n'est pas prêt à être commit)

Ensuite, 

~~~ bash
$ git add index.html

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ReadME.md
~~~

On voit maintenant que : 
- index.html est indexé
- ReadME.md ne l'est pas

Nous pouvons réaliser le commit : 

~~~ bash 
$ git commit -m "Ajout du fichier index.html"
[master (root-commit) 7028848] Ajout du fichier index.html
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html
~~~