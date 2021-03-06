# Use the base App Engine Docker image, based on debian jessie.
FROM gcr.io/google_appengine/debian8

# Install updates and dependencies
RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates libkrb5-dev imagemagick netbase && \
    apt-get clean && rm /var/lib/apt/lists/*_*

# Install the latest LTS release of nodejs
RUN mkdir /nodejs && curl https://nodejs.org/dist/v6.9.5/node-v6.9.5-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
ENV PATH $PATH:/nodejs/bin

# Install semver, as required by the node version install script.
# The use of --unsafe-perm is used here so that the installation is done
# as the current (root) user.  Otherwise, a failure in running 'npm install'
# (for example through a failure in a pre-or-post install hook) won't cause
# npm install to have a non-zero exit code.
RUN npm install --unsafe-perm semver

# Add the node version install script
ADD install_node /usr/local/bin/install_node

# Set common env vars
ENV NODE_ENV production

WORKDIR /app

# start
CMD ["npm", "start"]
