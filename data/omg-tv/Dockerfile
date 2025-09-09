# Usa Node 20 slim come base
FROM node:20-slim

# Installa pacchetti di sistema necessari
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git \
        python3 \
        python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Installa pacchetti Python
RUN pip3 install requests --break-system-packages

# Imposta la directory di lavoro
WORKDIR /app

# Clona il repository OMG-Premium-TV e copia i file
RUN git clone --branch main https://github.com/nzo66/OMG-Premium-TV.git /tmp/repo \
    && cp -r /tmp/repo/* /app/ \
    && rm -rf /tmp/repo

# Prepara directory e permessi
RUN mkdir -p /app/data /app/temp && \
    chmod 777 /app/temp && \
    chown -R node:node /app/data

# Installa le dipendenze Node
RUN npm install --production

# Imposta l’utente node per più sicurezza
USER node

# Espone la porta su cui gira OMG-Premium-TV
EXPOSE 10000

# Comando di avvio
CMD ["node", "index.js"]
