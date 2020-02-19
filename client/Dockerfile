FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build   

# The above builder step will create a build folder with
# all the necessary production build artifacts
# this folder will exist in /app/build

# The next steps are to get an nginx image and then
# copy our nginx conf file into the image
# and also copy the output from the step above into
# our nginx image (i.e. copy the /app/build folder in)

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
