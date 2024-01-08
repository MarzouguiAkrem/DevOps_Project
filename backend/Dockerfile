# Utiliser une image Node.js avec la version souhaitée
FROM node:14

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Copier le fichier package.json et package-lock.json pour installer les dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers de l'application dans le conteneur
COPY . .

# Exposer le port sur lequel le serveur Express écoute
EXPOSE 5000

# Commande de démarrage du serveur
CMD ["npm", "start"]
