# Utiliser une image Python officielle
FROM python:3.11-alpine

# Définir le répertoire de travail
WORKDIR /app

# Installer les dépendances système nécessaires à certaines bibliothèques Python
RUN apk add --no-cache gcc musl-dev python3-dev libffi-dev curl-dev

# Copier et installer uniquement les dépendances en premier
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copier le reste des fichiers de l'application
COPY . .

# Exposer le port 80
EXPOSE 80

# Lancer l'application
CMD ["python", "app.py"]

