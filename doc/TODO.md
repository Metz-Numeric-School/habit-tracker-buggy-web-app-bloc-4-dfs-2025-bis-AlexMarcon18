# TODO

Suite à un audit effectué en amont, voici les failles et les bugs qui ont été identifés comme prioritaire.

## FAILLES

- Des utilsateurs non admin ont des accès à l'interface de gestion des utilisateurs

_Fichier modifié_ : `config/routes.json`

- Ajout du guard `App\Guard\AdminGuard` sur `/admin/user` (ligne 32)
- Ajout du guard `App\Guard\AdminGuard` sur `/admin/user/new` (ligne 38)
- Ajout du guard `App\Guard\UserGuard` sur `/habits` (ligne 50)
- Ajout du guard `App\Guard\UserGuard` sur `/habits/create` (ligne 56)
- Ajout de la route `/habit/toggle` avec `App\Guard\UserGuard` (lignes 58-63)

- Les mots de passes ne sont pas chiffrée en base de données...

`src/Repository/UserRepository.php` (méthode `insert`)

- Ajout de `password_hash($data['password'], PASSWORD_DEFAULT)` avant insertion
- Les nouveaux mots de passe sont hashés avec l'algorithme bcrypt

`src/Controller/SecurityController.php` (méthode `login`)

- Remplacement de `$password == $user->getPassword()` par `password_verify($password, $user->getPassword())`
- Correction de la redirection `/user/dashboard` → `/dashboard` (ligne 22)
- Ajout de `exit` après la redirection vers `/dashboard` (ligne 48)
- Ajout d'un bloc `else` pour définir l'erreur si l'utilisateur n'existe pas (lignes 56-59)

`src/Controller/RegisterController.php`

- Correction de la redirection `/user/ticket` → `/dashboard` (ligne 52)

- Des injections de type XSS ont été détéctées sur certains formulaires

`src/Repository/HabitRepository.php`

- `find()` : Conversion en requête préparée avec `:id` (lignes 18-20)
- `findByUser()` : Conversion en requête préparée avec `:user_id` (lignes 25-27)
- `insert()` : Réécriture complète avec requête préparée (lignes 43-51)
- Utilisation de paramètres nommés `:user_id`, `:name`, `:description`
- On enleve la concatenation qui est une vulnérabilités

`src/Repository/UserRepository.php`

- `find()` : Conversion en requête préparée avec `:id` (lignes 18-20)
- `findByEmail()` : Conversion en requête préparée avec `:email` (lignes 25-27)

- On nous a signalé des injections SQL lors de la création d'une nouvelles habitudes

  - exemple dans le champs "name" : foo', 'INJECTED-DESC', NOW()); --

  `templates/member/dashboard/index.html.php`

  - Ligne 4 : `$_SESSION['user']['firstname']`
  - Ligne 50 : `$habit->getName()`
  - Ligne 51 : `$habit->getDescription()`

`templates/member/habits/new.html.php`

- Ligne 10 : `$_POST['habit']['name']`
- Ligne 12 : `$errors['name']`
- Ligne 18 : `$_POST['habit']['description']`

`templates/admin/user/index.html.php`

- Ligne 28 : `$user->getId()`
- Ligne 29 : `$user->getFirstname()` et `$user->getLastname()`
- Ligne 30 : `$user->getEmail()`

## BUGS

- Une 404 est détéctée lors de l'accès à l'URL `/habit/toggle`

**Route `/habit/toggle` manquante**

- Ajoutée dans `config/routes.json` (lignes 58-63)
- Pointe vers `App\Controller\Member\HabitsController::toggle()`
- Protégée par `UserGuard`

- Fatal error: Uncaught Error: Class "App\Controller\Api\HabitsController" lorsque l'on accède à l'URL `/api/habits`

**ATTENTION : certains bugs n'ont pas été listé**
