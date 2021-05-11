# Conduit Backend Fun
Primarily uses https://github.com/jsBlackBelt/microservices-realworld-app at this point. 
We could also use the older Express-based solution as well, we wanted to have some fun and try this new one!


Requires `docker-compose` and `yarn` to be installed (which will bring in git and docker on Debian). 

To run once cloned: 

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
cd microservices-realworld-app/
docker-compose up -d
```

Ports 3330, 3334, 3335, 3336 nd finally 3337 will need to be opened for the instance that you deploy. (In our case this is done in GCP for now, here: https://console.cloud.google.com/networking/firewalls/)

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn -y
cd apps
yarn
yarn start:all
```

# Note: in case you installed yarn from debian's packages: 

```bash
sudo apt remove cmdtest
sudo apt remove yarn
```

Test that it is running (on the instance):

```bash
curl localhost:3330/graphql
```

To test if this works (from your computer):

```bash
curl "${EXT_IP}":3330/api
```

