# Cachet Docker Image

This is the official repository of the [Docker image](https://hub.docker.com/r/cachethq/docker/) for [Cachet](https://github.com/cachethq/Cachet).

[Cachet](https://github.com/cachethq/Cachet) is a beautiful and powerful open source status page system, a free replacement for services such as StatusPage.io, Status.io and others.

For full documentation, visit the [Installing Cachet with Docker](https://docs.cachethq.io/docs/get-started-with-docker) page.

# Supporting Cachet

Cachet is a BSD-3-licensed open source project. If you'd like to support future development, check out the [Cachet Patreon](https://patreon.com/jbrooksuk) campaign.

# Docker Hub Automated build

`cachethq/docker` is available as a [Docker Hub Trusted Build](https://hub.docker.com/r/cachethq/docker/).

For a full list of Cachet versions released as Docker images  please see the [list of Docker hub tags](https://hub.docker.com/r/cachethq/docker/tags/).

The master branch and `cachethq/docker:latest` Docker automated build are a work in progress / development version of the upstream [Cachet](https://github.com/CachetHQ/Cachet) project. Use of `master` or `:latest` in a production environment is not recommended as it may change at any time.

Please use a [tagged Cachet Docker image release](https://github.com/CachetHQ/Docker/releases) or one of the tagged builds from https://hub.docker.com/r/cachethq/docker/tags/ with `docker pull cachethq/docker:2.2.1`.

# Testing

Pull requests must pass the [Bash Automated Testing System](https://github.com/sstephenson/bats) tests, which run on [Travis CI](https://travis-ci.org/CachetHQ/Docker) via located in the [test](test) directory.

Use `make test` to manually run the tests.


# Development of Cachet using this docker environment

1.  Clone the official repo of CachetHQ/Docker
  
  ```shell
  git clone https://github.com/cachethq/Docker.git cachet-docker
  cd cachet-docker
  git tag -l
  git checkout $LATEST_TAG
  ```
2. Clone the official repo of CachetHQ/Cachet here and do composer install
  
  ```shell
  git clone https://github.com/CachetHQ/Cachet.git
  ```

3. Setup the Cachet project
 
 ```shell
 cd Cachet
composer install
cp ../conf/.env.docker ./.env
cd ..
```

4. Edit the docker-compose.yml file

  ```yaml
  replace 
    build: . 
  with 
    image: cachethq/docker

  replace
    - /var/www 
  with 
    - ./Cachet/:/var/www/html/
  ```

5. Build and run the docker compose
  
  ```shell
  docker-compose up
  ```
  
6. Open new terminal and execute the following commands after getting container name via `docker ps`:
  
  ```shell
  docker exec -i cachetdocker_cachet_1  php artisan key:generate
  docker exec -i cachetdocker_cachet_1  php artisan app:install
  ```
