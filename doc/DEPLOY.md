# Procédure de Déploiement

Décrivez ci-dessous votre procédure de déploiement en détaillant chacune des étapes. De la préparation du VPS à la méthodologie de déploiement continu.

## Préparation du VPS

Premiere étape se connecter en root avec ssh à son vps

Vérifier dans cd /etc/ssh que le fichier de config sshd_config est bien en permitrootlogin yes et pas commenté si non décemmenter la ligne et passer en permit root login yes

Initialiser le dépôt distant sur votre vps:
cd /var
mkdir depot_git
cd depot_git
git init —bare

installation ensuite sur la vm de AApanel free edition avec cette ligne de commande: cd (pour aller à la racine)
Pour l’installation:
URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel

Récupérer ses informations:
URL, username, password et les garder
Mon AApanel:
aaPanel Internet Address: https://90.80.241.65:10524/527582ce
aaPanel Internal Address: https://172.17.4.17:10524/527582ce
username: 7nsoth42
password: 6bb329e8

## Méthode de déploiement

Acceder à l’url de aapanel,
lancer l’install d’un stack LNMP (linux nginx mysql php)

attendre la fin de l'installation

en attendant sur notre projet local:
initialiser un depot dit avec gitinit si besoin

ajouter le dépot distant que l'on a crée sur notre vps:

ici:
git remote add vps root@172.17.4.17:/var/depot_git

faire sont premier commit:

git add .
git status pour vérifier que l'on a ce qu'il faut dans notre premier push

git commit -m "Feat: Commit initial du déploiement de l'app"

ensuite on peu ajouter un tag avec:
git tag _NOM_DU_TAG_
git push -u vps _NOM_DU_TAG_

notre dépot distant se trouve alors bien sur notre VPS
une fois que notre dépot est bien push sur notre VPS:

celui ci est dans notre /var/depot_git
il faut le faire passer dans un dossier de site

Dans l'interface AApanel:
-> Add site
-> configurer son nom de domaine (dans mon cas: marcon-dfsgr1.local)
-> on peut mettre un ftp si besoin
-> on peut se config sa bdd en même temps (attention récuperer également les identifiant)
database settings: sql_marcon_dfsgr1_local
password: e91ded88aa47c

mettre sa version de php (8.3 selon l'énoncé)

une fois cela effectué on peut revenir sur notre connexion SSH avec notre VPS pour effectuer cette commande:

git --work-tree=/www/wwwroot/_NOM_DU_SITE_ --git-dir=/var/depot*git checkout -f \_NOM_DU_TAG*
pour moi:
git --work-tree=/www/wwwroot/marcon-dfsgr1.local --git-dir=/var/depot_git checkout -f 1.0.0

une fois effectué, notre dépot s'est cloné sur le repertoire de notre site,

dans la configuration du site web on peut aller dans repertoire de site et pointer le repertoire en cours d'execution sur public (il sera affiché si la manipulation avec la commande git --work-tree à bien fonctionné).
-> sur AApanel on peut laisser ou retirer l'anti xss attaque sui fait un peu baisser les performances.

il est possible que votre pc ne reconnaisse pas le dns pour cela:
sur votre vm:
root@debian:/etc# nslookup marcon-dfsgr1.local
Server: 172.17.0.254
Address: 172.17.0.254#53

Name: marcon-dfsgr1.local
Address: 172.17.4.17

et ensuite sur votre machine (local):
echo "172.17.4.17 marcon-dfsgr1.local" | sudo tee -a /etc/hosts

Enfin, sur votre vm, placer vous dans:
cd /www
cd wwwroot
cd _VOTRE_NOM_DE_DOMAINE_
et lancez un composer install pour avoir vos dépendances actives sur votre site si ce n'est pas déja fait

vous pouvez dorénavant acceder à votre site web
Il ne faudra pas oublier de créer votre base de données via l'interface database, modifier le .env de votre site si celui ci doit être modifié
acceder ensuite à votre SGBD (ici phpmyadmin)
et importer les tables et données dont vous avez besoin
