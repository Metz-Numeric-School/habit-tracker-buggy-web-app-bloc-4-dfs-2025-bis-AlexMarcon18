# Questions

Répondez ici aux questions théoriques en détaillant un maxium vos réponses :

1. Expliquer la procédure pour réserver un nom de domaine chez OVH avec des captures d'écran (arrêtez-vous au paiement) :

Accéder au site OVH
Allez sur https://www.ovhcloud.com/fr/
Cliquez sur "Domaines" dans le menu
Rechercher votre nom de domaine
Entrez le nom de domaine souhaité (ex: mon-site.fr)
Cliquez sur "Rechercher"
OVH vous affichera les extensions disponibles (.fr, .com, .net, etc.) avec les prix
Sélectionner votre domaine
Cliquez sur "Ajouter au panier" pour l'extension choisie
Vous pouvez ajouter plusieurs extensions
Choisir les options
DNS Anycast : inclus gratuitement (recommandé)
Protection WHOIS : masque vos informations personnelles (recommandé)
Durée : généralement 1 an (vous pouvez choisir 2-10 ans)
Compte client
Si vous avez déjà un compte : connectez-vous
Sinon : créez un compte avec votre email et informations
Informations de contact
Remplissez vos coordonnées (propriétaire, administratif, technique)
Ces infos sont obligatoires pour le registre

2. Comment faire pour qu'un nom de domaine pointe vers une adresse IP spécifique ?

Lorsque vous achetez un nom de domaine, le bureau d’enregistrement met à votre disposition un accès (via une interface de gestion) aux paramètres de la zone DNS en charge du domaine et des sous-domaines associés. Si votre registrar est votre hébergeur, la gestion de vos DNS ne pose pas problème. Si en revanche vous avez choisi un autre prestataire pour l’hébergement, il faudra intervenir pour transférer le contrôle des DNS vers votre hébergeur. Toute la gestion des paramètres importants de votre site sera ainsi centralisée chez l’hébergeur.

Si l’interface graphique varie selon les hébergeurs, le principe reste similaire. Vous devrez d’abord accéder au panneau d’administration de votre domaine chez le registrar, ainsi qu’à votre nouveau compte d’hébergement. Il vous faudra récupérer la liste des DNS de votre hébergeur, de manière à entrer leurs noms dans le champ dédié sur l’interface de votre registrar. Sur le panneau de contrôle, vous pouvez changer les DNS d’un domaine ou de plusieurs. Un nom de domaine devra être associé à au moins deux DNS. Le plus souvent, un temps de propagation est nécessaire pour que la nouvelle configuration soit prise en compte. Celui-ci dure en moyenne 24 heures, mais il peut varier de quelques heures seulement à 3 jours entiers. Il n’est pas utile de s’inquiéter avant 72 heures ! Les DNS resteront désormais configurables, au besoin, sur la plateforme de votre hébergeur.

3. Comment mettre en place un certificat SSL ?

Dans aaPanel :
Allez dans "Website"
Sélectionnez votre site marcon-dfsgr1.local (ou votre nouveau domaine)
Cliquez sur "SSL"
Let's Encrypt :
Onglet "Let's Encrypt"
Entrez votre email
Sélectionnez les domaines (cochez mon-domaine.fr et www.mon-domaine.fr)
Cliquez sur "Apply"
Configuration automatique :
aaPanel va automatiquement :
Générer le certificat
L'installer
Configurer le renouvellement automatique (tous les 90 jours)
Forcer HTTPS :
Activez l'option "Force HTTPS" dans aaPanel
Cela redirigera automatiquement HTTP → HTTPS
(attention cependant pour le faire depuis AApanel, il faut un compte avec l'edition pro)
