# Utilisation de l'image officielle Node.js Alpine
FROM node:21-alpine

# Définition du répertoire de travail
WORKDIR /app

# Copie des fichiers package.json et package-lock.json avant installation
COPY package*.json ./

# Installation des dépendances
RUN npm install --omit=dev

# Copie du reste de l'application
COPY . .

# Exposition du port 80
EXPOSE 80

# Commande de démarrage
CMD ["node", "server.js"]
