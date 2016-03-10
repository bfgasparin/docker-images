FROM node:0.10

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app
ONBUILD COPY package.json /usr/src/app/
ONBUILD COPY .npmrc /usr/src/app/
# We copy bower files to fix the lack of control over when the ONBUILD trigger fires
ONBUILD COPY bower.json /usr/src/app/
ONBUILD COPY .bowerrc /usr/src/app/
ONBUILD RUN npm install
ONBUILD COPY . /usr/src/app

CMD [ "npm", "start" ]