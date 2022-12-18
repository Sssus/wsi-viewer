FROM node:12-alpine AS builder

WORKDIR /app

COPY package.json ./
RUN npm config set package-lock false
RUN npm install --no-optional
COPY . ./
RUN npm run build

EXPOSE 5000
ENV HOST=0.0.0.0

#CMD ["npm", "run", "dev"]
CMD ["npm","start"]