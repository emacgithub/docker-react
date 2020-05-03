# Build phase. Label this base image as `builder` stage
FROM node:alpine AS builder
# Set directory where all following commands will execute in the container
WORKDIR '/app'
# Copy package.json to the WORKDIR
COPY package.json .
# Install dependencies in the WORKDIR i.e. node_modules directory
RUN npm install
# Copy over all the source code
COPY . .
# Build the production files.  Will create a build folder in the WORKDIR
RUN npm run build

# Run phase  See nginx docker hub documentation for more details
# Use nginx as base image
FROM nginx
# Copy from the `builder` stage from the /app/build directory to the nginx directory that will display the content
COPY --from=builder /app/build /usr/share/nginx/html
# No need to specify a CMD or ENTRYPOINT as the nginx container will start automatically