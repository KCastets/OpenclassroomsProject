# Projet de prise en main de Git

Il s'agit d'un projet fictif de site internet pour prendre en main Git et GitHub.
Dans ce ReadMe, il y aura les commandes suivies pas à pas pour : 
- Initialiser l'envirronement de travail Git en local
- Initialiser le dépot Git
- Création de clés SSH
- Suivre le cycle de vie du développement du projet fictif.
    * Les bases
    * Les branches   

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
Nous allons devoir les mettre en commun.

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

## Correction d'erreurs

* Supprimer une branche : 
~~~ bash
$ git branch brancheTest
$ git branch
  brancheTest
* master

$ git branch -d brancheTest
Deleted branch brancheTest (was ef8c30d).

$ git branch
* master
~~~

* Modification de fichier sur une mauvaise branche
~~~ bash
$ git branch
* main

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   fichier.txt

$ git stash
Saved working directory and index state WIP on master: ef8c30d FirstFile

$ git status
On branch master
nothing to commit, working tree clean

$ git branch branche1

$ git checkout branche1
Switched to branch 'branche1'

$ git stash list
stash@{0}: WIP on master: ef8c30d FirstFile

$ git stash apply stash@{0}
On branch branche1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   fichier.txt

$ git commit -m "Commit after stash"
[branche1 5784765] Commit after stash
 1 file changed, 1 insertion(+)
 create mode 100644 fichier.txt
~~~

* Erreur : Modification et Commit sur la mauvaise branche

Avec 'git log' on peut identifier les derniers commits.
 ~~~ bash
$ git log
commit b0249c88c2f9cf5e3a1686c416c1fd02eebf6027 (HEAD -> master)
Author: KCastets <killiancastets@gmail.com>
Date:   Thu Jan 22 15:01:22 2026 +0100

    j'ai tout supprimée

commit 1fd8972981e433a57cadfbff6a3b33c7bf0bfba9 (branche1)
Author: KCastets <killiancastets@gmail.com>
Date:   Thu Jan 22 14:58:12 2026 +0100

    Ceci est un commit rempli de trop d'erreurs...

$ git reset --hard HEAD^
~~~
Ici, on a supprimé le commit.
Il faut maintenant aller se mettre sur la branche correcte et l'appliquer de nouveau

~~~ bash
$ git reset --hard id_8_first_caracters
~~~

* Modifier un message de commit

~~~ bash
$ git commit --amend -m "Nouveau message
~~~

* Oublie de fichier à mettre dans un commit : 

~~~ bash
$ git add fichierOublie.txt
$ git commit --amend --no-edit
~~~
