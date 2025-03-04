#We can have 2 dockerfiles one is for builder, we can copy the output from builder into 2nd dockerfile and run it, we can save some image space using this


FROM node:20.18.3-alpine3.21 AS builder
WORKDIR /opt/backend
COPY package.json ./
COPY *.js ./
RUN npm install

# Above instructions will build the image

#we are copying the /opt/backend directory from the above image
FROM node:20.18.3-alpine3.21
RUN addgroup -S expense && adduser -S expense -G expense && \
    mkdir /opt/backend && \
    chown -R expense:expense /opt/backend
ENV DB_HOST="mysql"
WORKDIR /opt/backend
USER expense
COPY --from=builder /opt/backend /opt/backend
CMD ["node", "index.js"]

#We can have 2 dockerfiles one is for builder, we can copy the output from builder into 2nd dockerfile and run it, we can save some image space using this












# optimizing layers

#1. less number of layers faster builds, because number of intermediate containers are less
#you can club multiple instructions into single instruction
#2. keep the frequently changing instructions at the bottom of Dockerfile (pile of bread example)

#FROM node:20.18.3-alpine3.21
#RUN addgroup -S expense && adduser -S expense -G expense && \
 #   mkdir /opt/backend && \
  #  chown -R expense:expense /opt/backend
#WORKDIR /opt/backend
#ENV DB_HOST=mysql
#USER expense
#COPY package.json .
#COPY *.js .
#RUN npm install
#CMD ["node", "index.js"]