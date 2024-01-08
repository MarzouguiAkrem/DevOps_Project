# Utiliser une image Node.js avec la version souhaitée
FROM node:14

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Copier le fichier package.json et package-lock.json pour installer les dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier les fichiers de l'application dans le conteneur
COPY . .

# Construire l'application pour la production
RUN npm run build

# Exposer le port sur lequel l'application fonctionne
EXPOSE 3000

# Commande de démarrage de l'application
CMD ["npm", "start"]
