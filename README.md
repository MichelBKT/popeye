
# Projet Docker avec PostgreSQL, Redis et un Worker Java

Ce projet utilise Docker pour orchestrer plusieurs services :

- PostgreSQL comme base de données

- Redis comme système de mise en cache

- Un worker en Java pour traiter certaines tâches en arrière-plan

- Un service d'application pour interagir avec la base de données et Redis



## Pré-requis

Docker desktop installé sur votre machine


## Installation

Installation et exécution

Clonez ce dépôt sur votre machine locale

```bash
  git clone
```
Assurez-vous d'avoir un fichier .env à la racine du projet contenant :
```bash
    POSTGRES_USER=user
    POSTGRES_PASSWORD=password
    POSTGRES_DB=mydatabase
    REDIS_HOST=redis
    REDIS_PORT=6379
                  *********** les valeurs sont à modifier*****************
```
Construisez et démarrez les conteneurs :
```bash
  docker-compose up --build
```



## Déploiement Docker

#### PostgreSQL

Le service PostgreSQL est configuré dans docker-compose.yml sous le nom db.

Il expose le port 5432.

La base de données est initialisée avec un script SQL présent à la racine du projet /docker-entrypoint-initdb.d/.

#### Redis

Le service Redis est configuré sous le nom redis.

Il est accessible sur le port 6379.

#### Worker Java

Le Worker Java est développé en tant que service worker et compile un fichier .java en .jar avant de l'exécuter.

Compilation :

javac -d out Worker.java
jar cfe Worker.jar worker.Worker -C out .

Exécution :

java -jar worker-jar-with-dependencies.jar




## Support

#### Erreur relation "votes" does not exist

Assurez-vous que la table votes est bien créée :

        CREATE TABLE votes (
            id SERIAL PRIMARY KEY,
            user_id INT NOT NULL,
            post_id INT NOT NULL,
            vote_type VARCHAR(10),
            created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
        );

Importez le fichier SQL si besoin.

#### Erreur getaddrinfo ENOTFOUND postgres

Assurez-vous que votre service PostgreSQL est bien nommé db dans docker-compose.yml et non postgres.

#### Arrêt et suppression des conteneurs + données
```bash
  docker-compose down -v
```


## Author

- [@MichelBKT](https://www.github.com/MichelBKT)


