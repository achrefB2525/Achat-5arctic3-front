# Utiliser une image de base avec Node.js et npm pré-installés
FROM node:14-alpine AS build

# Définir le répertoire de travail à l'intérieur du conteneur
WORKDIR /app

# Copier les fichiers de l'application (y compris package.json) dans le conteneur
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier tous les fichiers de l'application dans le conteneur
COPY . .

# Construire l'application Angular (peut nécessiter des ajustements selon votre configuration)
RUN npm run build

# Utiliser une image Nginx comme image de production
FROM nginx:alpine

# Copier les fichiers construits de l'application dans le répertoire approprié de l'image Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exposer le port 80 (par défaut pour Nginx)
EXPOSE 80
EXPOSE 8089

# Commande à exécuter lorsque le conteneur démarre
CMD ["nginx", "-g", "daemon off;"]
