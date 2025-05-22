# Conteneurisation d'une Application Full Stack (VueJS, Flask, MariaDB)

Ce projet consiste en la conteneurisation d'une application full stack utilisant Vue.js pour le front-end, Flask pour le back-end, et MariaDB pour la base de données.

## Images Docker

Les images Docker sont disponibles sur DockerHub aux URLs suivantes :
- Front-end (Vue.js + NGINX) : [rebzu/vuejs-app](https://hub.docker.com/r/rebzu/vuejs-app)
- Back-end (Flask) : [rebzu/flask-app](https://hub.docker.com/r/rebzu/flask-app)
- Base de données (MariaDB) : [rebzu/mariadb-server](https://hub.docker.com/r/rebzu/mariadb-server)


## Instructions d'exécution

### 1. Créer un réseau Docker

```bash
docker network create app-network
```

### 2. Lancer le conteneur MariaDB

```bash
docker run -d \
  --name mariadb-server \
  --network app-network \
  -v mariadb_data:/var/lib/mysql \
  -p 3306:3306 \
  rebzu/mariadb-server
```

### 3. Lancer le conteneur Flask

```bash
docker run -d \
  --name flask-app \
  --network app-network \
  -p 5000:5000 \
  rebzu/flask-app
```

### 4. Lancer le conteneur Vue.js

```bash
docker run -d \
  --name vuejs-app \
  --network app-network \
  -p 80:80 \
  rebzu/vuejs-app
```

### 5. Tester l'application

Pour tester l'API :
```bash
# Ajouter un message
curl -X POST http://localhost:5000/api/messages -H "Content-Type: application/json" -d '{"name": "Romain Lenoir", "message": "Ceci est un message de test."}'

# Récupérer les messages
curl -X GET http://localhost:5000/api/messages
```

Pour accéder à l'interface web, ouvrez un navigateur et accédez à `http://localhost`.