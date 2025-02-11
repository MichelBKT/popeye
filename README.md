# Projet Docker avec PostgreSQL, Redis et Worker

Ce projet utilise Docker et Docker Compose pour orchestrer une application composée de plusieurs services :
- **PostgreSQL** : Base de données principale
- **Redis** : Cache et file d'attente
- **Worker** : Service de traitement en Java
- **Poll** : Service basé sur Flask
- **Result** : Service basé sur Node.js

## Prérequis
- Docker et Docker Compose installés
- Un fichier `.env` contenant les variables d'environnement pour PostgreSQL et les autres services

## Installation
Clonez ce dépôt et accédez au dossier du projet :
```sh
  git clone <repository_url>
  cd <project_directory>
```

## Configuration
Créez un fichier `.env` à la racine du projet avec :
```sh
    POSTGRES_USER=your_username
    POSTGRES_PASSWORD=your_password
    POSTGRES_DB=your_database
    DB_PORT=5432
    REDIS_HOST=redis
    REDIS_PORT=6379
```

## Lancer les services
Démarrez les conteneurs avec :
```sh
  docker-compose up --build -d
```
Cela construira et démarrera tous les services avec les réseaux `poll-tier`, `result-tier` et `back-tier` définis dans `docker-compose.yml`.

## Vérifier les logs
Vous pouvez consulter les logs des services en temps réel :
```sh
  docker-compose logs -f
```

## Accéder aux services
- **PostgreSQL** : `localhost:5432`
- **Redis** : `localhost:6379`
- **Poll (Flask)** : `http://localhost:5000`
- **Result (Node.js)** : `http://localhost:5001`

## Vérifier les variables d'environnement dans un conteneur
Par exemple, pour `worker` :
```sh
  docker exec -it worker env | grep DB_
```
Vous devez voir :
```
DB_HOST=db
DB_PORT=5432
DB_USER=your_username
DB_PASSWORD=your_password
DB_NAME=your_database
```
Si `DB_PORT` est `null`, vérifiez votre `.env` et `docker-compose.yml`.

## Arrêter et nettoyer les conteneurs
Pour stopper les services :
```sh
  docker-compose down
```
Pour supprimer les volumes de données :
```sh
  docker-compose down -v
```

## Dépannage
- **Erreur `relation \"votes\" does not exist`** : Vérifiez que la migration SQL a bien été appliquée.
- **`ENOTFOUND postgres`** : Vérifiez que le service `db` est bien défini dans `docker-compose.yml`.
- **Le worker affiche `JDBC URL invalid port number: null` ?** Assurez-vous que `DB_PORT=5432` est bien défini dans `docker-compose.yml` et `.env`.
- **Vérifiez avec `System.getenv("DB_PORT")` dans le code Java pour voir s'il est bien récupéré.**


## Author

- [@MichelBKT](https://www.github.com/MichelBKT)

