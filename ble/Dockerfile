FROM node

#install packages
# RUN npm install bluetooth bluez libbluetooth-dev libudev-dev
# RUN apt-get install bluetooth bluez libbluetooth-dev libudev-dev

RUN apt-get -q update && apt-get install -yq --no-install-recommends \
	build-essential \
	&& apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y bluetooth bluez libbluetooth-dev libudev-dev \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Defines our working directory in container
WORKDIR /usr/src/app

# Copies the package.json first for better cache on later pushes
COPY package.json /usr/src/app 

# This install npm dependencies on the balena build server,
# making sure to clean up the artifacts it creates in order to reduce the image size.
# RUN JOBS=MAX npm install --nouislider --production --unsafe-perm && npm cache verify && rm -rf /tmp/*
RUN npm install --nouislider --production --unsafe-perm && npm cache verify && rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY . .

# Enable udevd so that plugged dynamic hardware devices show up in our container.
ENV UDEV=1

# server.js will run when container starts up on the device
CMD ["npm", "start"]