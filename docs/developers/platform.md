# OpenSpending platform

The OpenSpending platform has been designed as a set of loosely coupled components, each performing distinct functions related to the platform as a whole. For an overview of the platform components, [see here](../developers/).

Local installation and remote deployment of OpenSpending is orchestrated with Docker; specifically [Docker Compose](https://docs.docker.com/compose/). There are configurations available that are tailored to each target.

## Resources

As well as the main code repository for the [OpenSpending platform](https://github.com/openspending/openspending), all the components are pre-built on Docker hub. See the [OpenSpending organization on Docker Hub](https://hub.docker.com/u/openspending/) for all available images.

## Installation

### Docker

#### Installation

Before getting started, you must ensure that you have the full suite of Docker tools installed on your system. Installing [Docker Toolbox](https://www.docker.com/products/docker-toolbox) is the easiest way to ensure this.

#### Validation

Once you have installed Docker Toolbox (or if you already have it installed), ensure that you have the versions that we support for OpenSpending by running the following in your terminal:

- `docker -v` *must be* `1.10.0` or higher
- `docker-compose -v` *must be* `1.6.0` or higher
- `docker-machine -v` *must be* `0.6.0` or higher

#### Installing Docker-Machine

__Note__: If you are running linux, you can skip the whole part about `docker-machine`.

If you already had Docker Machine installed, and you *upgraded* Docker Toolbox when following the steps above, then run the following to get your Docker Machine image updated:

- `docker-machine upgrade`

Now make sure that your shell session has the environment variables needed by `docker-machine`.

The simple way to do this is by running this command:

- `eval $(docker-machine env default)`

Alternatively, add the following to your `.bash_profile`, `.profile`, `.bashrc` or equivalent (based on the system you run):

```
export DOCKER_TLS_VERIFY=1
export DOCKER_MACHINE_NAME=default
export DOCKER_CERT_PATH=$HOME/.docker/machine/machines/$DOCKER_MACHINE_NAME
export DOCKER_HOST=tcp://$(docker-machine ip $DOCKER_MACHINE_NAME):2376
```

Then source your shell config (adjust based on the file you just added the configuration to):

- `source ~/.bash_profile`

### OpenSpending

#### Hosts

OpenSpending is a number of services running on different sub-directories, and some services require a "real" domain to work (example: authentication). So, we want to create a record in the `hosts` file of the computer that maps the Docker Machine IP address to a host name.

Get your Docker Machine IP address with (it is usually `192.168.99.100`):

- `docker-machine ip default`

Then, with that IP as `{DOCKER_MACHINE_IP}`, add the following to your `/etc/hosts` file (or the [Windows equivalent](http://superuser.com/questions/525688/whats-the-windows-equivalent-of-etc-hosts)):

- `{DOCKER_MACHINE_IP} fakes3 dev.openspending.org`

#### Code

Once your hosts file is configured correctly, clone the code:

- `git clone https://github.com/openspending/openspending`

Now, let's bootstrap the whole development environment:

```
# Get in place
cd openspending # or, the directory that holds the cloned code

# Clone supporting code for development purposes
repos/clone_all.sh

# Boot up using the development configuration
cd docker-config && ./docker-start-dev.sh
```

When complete, visit the following URLs in your browser:

- [Packager](https://dev.openspending.org/packager)
- [Viewer](https://dev.openspending.org/viewer)
- [API](https://dev.openspending.org/api)

#### Hacking

You can modify the code under `repos/` and rerun `./docker-start-dev.sh` to see the changes take place.

#### Deployment

Deploying to a remote server is essentially the same, but requirements some prior configuration via environment variables.

Ensure you can access your remote server via SSH. If you can, then proceed.

##### Environment variables

The following environment variables need to be defined *locally* before proceeding to bootstrap the production environment:

- `OS_DB_HOST`: the OpenSpending DB host name
- `OS_DB_PWD`: the OpenSpending DB connection password
- `OS_API_ENGINE`: the OpenSpending DB connection string
- `OS_CONDUCTOR_ENGINE`: the OpenSpending DB connection string
- `OS_ACCESS_KEY_ID`: the access key for S3
- `OS_SECRET_ACCESS_KEY`: the access secret key for S3
- `OS_STORAGE_BUCKET_NAME`: the bucket name on S3
- `OS_PACKAGER_CONDUCTOR_HOST`: the domain for the conductor instance to use in the Packager
- `OS_PACKAGER_BASE_PATH`: the base path for the Packager app to serve from
- `OS_VIEWER_API_HOST`: the domain of the API instance to use in the Viewer
- `OS_VIEWER_AUTH_HOST`: the domain of the Auth server instance to use in the Viewer
- `OS_VIEWER_BASE_PATH`: the base path for the Viewer app to serve from
- `OS_VIEWER_SEARCH_HOST`: the domain of the Search API instance to use in the Viewer

##### Bootstrapping

The current flow works for the Open Knowledge International OpenSpending instance. Until improve the generic setup flow, you'll have to get your hands dirty and at least modify the `forward-ports.sh` script, and possibly others.

- Create a connection to the server and tunnel some of your local ports to it:
  - `docker-config/forward-ports.sh`
- Create the `oslocal` docker machine:
    - `docker-machine create -d generic --generic-ip-address 127.0.0.1 --generic-ssh-port 2222 --generic-ssh-user <YOUR-USERNAME> oslocal`
- Load the settings of this machine to the shell: `eval $(docker-machine env oslocal)`.
- Build the containers from scratch to make sure you're deploying the latest code `docker-compose -f production.yml build --no-cache`
- Start the docker containers on the remote server:
    - `docker-config/docker-start-prod.sh`


### Troubleshooting

- In some cases, the local virtual machine may have DNS configuration issues, in which case, add `nameserver 8.8.8.8` tp the guest `/etc/hosts`
- If you are having problems with the setup not working due to download errors, certificate errors, or other inexplicable errors, try running `docker-machine upgrade && docker-machine regenerate-certs` and try again.

### Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the Viewer [can be found here](https://github.com/openspending/openspending/issues), labeled "Viewer". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
