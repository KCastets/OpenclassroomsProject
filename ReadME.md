# Projet de prise en main de Git

Il s'agit d'un projet fictif de site internet pour prendre en main Git et GitHub.
Dans ce ReadMe, il y aura les commandes suivies pas à pas pour : 
- Initialiser l'envirronement de travail Git en local
- Initialiser le dépot Git
- Création de clés SSH
- Suivre le cycle de vie du développement du projet fictif.
    * Les bases
    * Les branches   
- Récupérer un projet existant

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

## Création de clés SSH

Pour générer des clés SSH : 

~~~bash
$ ssh-keygen -t ed25519 -C "killiancastets@gmail.com" # Générer de nouvelles clés
$ eval "$(ssh-agent -s)" # Vérifier que l'agent SSH fonctionne
$ ssh-add ~/.ssh/id_ed25519 # Ajouter les clés à l'agent SSH
$ cat ~/.ssh/id_ed25519.pub # Visualiser la clé Publique.
~~~

Il faut ensuite utiliser les clés SSH dans ce tuto de GitHub pour ajouter la clé publique à GitHub:
https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=linux

## Cycle de développement

### Les Bases
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

Maintenant, nous voulons relier notre repository GitHub au dépot Git.
Pour cela, il faut récupérer le lien SSH du repo sur GitHub, par exemple: git@github.com:KCastets/OpenclassroomsProject.git

~~~ bash
$ git remote add origin git@github.com:KCastets/OpenclassroomsProject.git # Lier le repo GitHub au dépot Git
$ git branch -M main # Choisir la branche sur laquelle réaliser le commit
$ git push -u origin main # Envoyer nos modifications réalisées sur le dépot Git vers le repo GitHub
~~~

### Les branches

En l'état actuel du projet, nous avons seulement notre branche principales, main : 

~~~ bash 
$ git branch
* main
~~~

Sur notre site internet, nous vopulons créer une fonctionnalité de cagnotte. Un bonne pratique est d'avoir une branche par fonctionnalité. Donc nous allons créer une branche pour developper notre cagnotte : 

~~~ bash 
$ git branch cagnotte
$ git branch
  cagnotte
* main
~~~

L'astérisque montre la branche courante.
Pour se déplacer sur la branche cagnotte, nous faisons : 

~~~ bash 
$ git checkout cagnotte

Switched to branch 'cagnotte'
~~~

Nous pouvons developper notre fonctionnalité fictive : 

~~~ bash 
$ touch cagnotte.txt #Ajout du fichier contenant la fonctionnalité cagnotte
$ git add cagnotte.txt
$ git commit -m "Realisaion de la cagnotte"
[cagnotte aad249e] Realisaion de la cagnotte
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cagnotte.txt
~~~

Notre branche cagnotte contient donc un commit différent du dernier commit réalisé sur la branche main.
Nous allons devoir l'envoyer sur le repo GitHub : 

~~~ bash 
$ git push -u origin cagnotte
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 361 bytes | 361.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'cagnotte' on GitHub by visiting:
remote:      https://github.com/KCastets/OpenclassroomsProject/pull/new/cagnotte
remote:
To github.com:KCastets/OpenclassroomsProject.git
 * [new branch]      cagnotte -> cagnotte
branch 'cagnotte' set up to track 'origin/cagnotte'.
~~~

Puis mettre en commun les deux branches.
Il faut se placer dans la branche qui va recevoir les modifications.

~~~ bash
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

$ git branch
  cagnotte
* main

$ git merge cagnotte
Updating f162c27..c8c769d
Fast-forward
 ReadME.md    | 61 ++++++++++++++++++++++++++++++++++++++++
 cagnotte.txt |  0
 2 files changed, 61 insertions(+)
 create mode 100644 cagnotte.txt
~~~

## Récupérer un projet existant

Pour récupérer un projet existant il faut réaliser un clone.
Pour cela, il faut se positionner dans le terminal à la racine contenant nos projets.

~~~ bash
~$ cd Git
~/Git$ git clone https://github.com/OpenClassrooms-Student-Center/7162856-G-rez-Git-et-GitHub.git

Cloning into '7162856-G-rez-Git-et-GitHub'...
remote: Enumerating objects: 25, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 25 (delta 7), reused 3 (delta 3), pack-reused 9 (from 1)
Receiving objects: 100% (25/25), done.
Resolving deltas: 100% (8/8), done.

~/Git$ cd  7162856-G-rez-Git-et-GitHub/
~/Git/7162856-G-rez-Git-et-GitHub$ ls
README.md  index.html  style.css
~~~

Dans le cas où on possède déjà, en local, un projet et que celui-ci a subit des modifications : 

~~~ bash
~/Git/7162856-G-rez-Git-et-GitHub$ git pull origin main
From https://github.com/OpenClassrooms-Student-Center/7162856-G-rez-Git-et-GitHub
 * branch            main       -> FETCH_HEAD
Already up to date.
~~~

## Création d'une Pull Request

Lorsque l'on participe à des projets avec plusieurs développeur, il devient nécessaire de réaliser des merge de code plus coordonnées. Pour cela, lorsqu'on termine de développer notre feature, il convient de faire un pull request : Une demande de merge en 2 étapes, permettant de s'assurer que l'on écrase pas le code du voisin.

~~~ bash
$ git branch update-color
$ git checkout update-color
M       ReadME.md
M       index.html
M       styles.css
Switched to branch 'update-color'

$ git add .
$ git status
On branch update-color
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   ReadME.md
        modified:   index.html
        modified:   styles.css

$ git commit -m "A
jout du titre h2 et son css"
[update-color 9c21caa] Ajout du titre h2 et son css
 3 files changed, 65 insertions(+), 2 deletions(-)

$ git push -u origin update-color
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 12 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 1.47 KiB | 302.00 KiB/s, done.
Total 5 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote:
remote: Create a pull request for 'update-color' on GitHub by visiting:
remote:      https://github.com/KCastets/OpenclassroomsProject/pull/new/update-color
remote:
To github.com:KCastets/OpenclassroomsProject.git
 * [new branch]      update-color -> update-color
branch 'update-color' set up to track 'origin/update-color'.


~~~