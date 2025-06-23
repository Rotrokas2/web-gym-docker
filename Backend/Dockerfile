FROM node:16-alpine

WORKDIR /app

# Copiamos solo package.json y package-lock.json (si existe) primero para cachear las capas
COPY package*.json ./

# Instalamos dependencias (incluye devDependencies porque no usas --production)
RUN npm install --save-dev codecov

# Ahora copiamos el resto del código y tests
COPY . .

# Exponemos el puerto para el servidor
EXPOSE 3000

# Comando por defecto para producción
CMD ["node", "server.js"]
