1.
Créer une base de donnée "db_1" qui contient une table "users" qui correspond à la database que nous avons créé dans le cours précédent sur express:

const db_user = {
  alice: '123',
  bob: '456',
  charlie: '789',
}
Créez les bons champs et donner les bons types à chaque champs. N'oubliez pas un champ "id" qui correspondra à la clé primaire.
Ensuite afficher toutes les lignes de la table "users" de la base de donnée "db_1".
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- psql -d postgres -U db_user
- postgres=> CREATE DATABASE db-1  output : db_1=>
-  db_1=> CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(30), password VARCHAR(30)); output: CREATE TABLE
- db_1=> INSERT INTO users (name, password) VALUES ('alice', '123'),('bob', '456'),('charlie', '789'); 
output: INSERT 0 3

2.
Ajouter 3 utilisateurs 'dan', 'eve', 'faythe' qui auront respectivement les password '101112', '131415', '161718'.
Affichez toutes les lignes de la table "users" de la base de donnée "db_1".
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> INSERT INTO users (name, password) VALUES ('dan', '101112'),('eve', '131415'),('faythe', '161718');
output: INSERT 0 3
- db_1=> SELECT * FROM users;
output: 
id |  name   | password
----+---------+----------
  1 | alice   | 123
  2 | bob     | 456
  3 | charlie | 789
  4 | dan     | 101112
  5 | eve     | 131415
  6 | faythe  | 161718
(6 rows)

3.
Affichez toutes les lignes de la table "users" de la base de donnée "db_1" dont le password possède plus de 3 caractères. Pour cela il vous faudra utiliser la fonction LENGTH.
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> SELECT * FROM users WHERE LENGTH(password) > 3;
output: 
id |  name  | password
----+--------+----------
  4 | dan    | 101112
  5 | eve    | 131415
  6 | faythe | 161718
(3 rows)

4. 
Modifiez la table "users" afin d'ajouter une nouvelle colonne "bio" qui contiendra une description a propos de l'utilisateur. Ce champ "bio" sera du texte avec un nombre de caractères illimités et sa valeur par défaut sera "Hello, world!".
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> ALTER TABLE users ADD COLUMN bio TEXT DEFAULT 'Hello,World!';
output : ALTER TABLE

5.
Modifiez toutes les lignes existantes pour que la "bio" de chacun affiche, "Hello, i am PRENOM_DU_USER".
Il faudra remplacer PRENOM_DU_USER par le véritable login de l'utilisateur.
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> UPDATE users  SET bio = 'Hello, i am ' ||(name);
output: UPDATE 6

6.
Afficher les 2 lignes qui ont les "id" les plus grands par ordre décroissant.
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> SELECT * FROM users ORDER BY id DESC LIMIT 2;
output : 
id |  name  | password |        bio
----+--------+----------+--------------------
  6 | faythe | 161718   | Hello, i am faythe
  5 | eve    | 131415   | Hello, i am eve
(2 rows)

7.
Afficher toutes les lignes de la table "users" dont les "id" sont impairs par ordre croissant.
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> SELECT * FROM users WHERE id%2 = 1;
output : 
 id |  name   | password |         bio
----+---------+----------+---------------------
  1 | alice   | 123      | Hello, i am alice
  3 | charlie | 789      | Hello, i am charlie
  5 | eve     | 131415   | Hello, i am eve
(3 rows)

8.
Effacez toutes les lignes de la table "users dont les "id" sont pairs. Affichez toutes les lignes de la table users.
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> DELETE FROM users WHERE id%2=0;
output: DELETE 3
- db_1=> SELECT * FROM users;
output: 
id |  name   | password |         bio
----+---------+----------+---------------------
  1 | alice   | 123      | Hello, i am alice
  3 | charlie | 789      | Hello, i am charlie
  5 | eve     | 131415   | Hello, i am eve
(3 rows)

9.
Effacer la TABLE "users".
Effacer la DATABASE "db_1".
Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

- db_1=> DROP TABLE users;
output: DROP TABLE
- postgres=> DROP DATABASE db_1;
output: DROP DATABASE