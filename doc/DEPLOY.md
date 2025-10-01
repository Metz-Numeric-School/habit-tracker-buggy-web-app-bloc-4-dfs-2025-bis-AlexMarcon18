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

Todo...
