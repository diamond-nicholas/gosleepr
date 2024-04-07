FROM node:alpine AS development

WORKDIR /usr/src/app

COPY package.json package-lock.json ./

# Install project dependencies using npm
RUN npm install

COPY . .

# Build the application
RUN npm run build

FROM node:alpine AS production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src/app

COPY package.json package-lock.json ./

# Install only production dependencies using npm
RUN npm install --production

# Copy built files from development stage
COPY --from=development /usr/src/app/dist ./dist

CMD [ "node", "dist/apps/reservations/main" ]
