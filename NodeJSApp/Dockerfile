# ---- Base Node ----
FROM node:carbon AS base
# Create app directory
WORKDIR /app

# ---- Dependencies ----
FROM base AS dependencies  
# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
# install app dependencies including 'devDependencies'
RUN npm install


# ---- Copy Files/Build ----
FROM dependencies AS build  
WORKDIR /app
# Copy src folder to /app
COPY src /app

# --- Release with Alpine ----
FROM node:8.11.2-alpine AS release  
# Create app directory
WORKDIR /app
COPY --from=dependencies /app/package*.json ./
# Install app dependencies
RUN npm install --only=production
COPY --from=build /app ./
#CMD ["serve", "-s", "dist", "-p", "8080"]
CMD ["node", "index.js"]