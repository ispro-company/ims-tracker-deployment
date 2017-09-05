# Deployment of ims-tracker application using docker-compose

This deployment process:

- checkouts desired version of ims-tracker application from the git repository
- launches postgress database to serve as backed for ims-tracker
- runs ims-tracker application

## Requirements

- Docker >= 17.06
- docker-compose >= 1.14.0
- ssh key capable of checking out ims-tracker source code under path $HOME/.ssh/id_rsa

## Configuration
File `ims-tracker.env` contains variables that need to be set prior to successful deployment. Database credentials needs to be the same as configured in ims-tracker.

## Running

To start the deployment process and launch ims-tracker on port `9090` using grails environment `test`: 

~~~
GRAILS_PORT=9090 GRAILS_ENV=test docker-compose up -d
~~~

To stop the deployment run:
~~~
GRAILS_PORT=9090 GRAILS_ENV=test docker-compose down -v
~~~

## Data Persistence
Upon starting there will be two directories created on the host filesystem:

- `$PWD/attachments` where tracker attachments are stored
- `$PWD/data-persistence` - where Postgres database is stored

Thanks to that, you can remove or restart the containers without loosing the state of the application.

## Debugging

You can attach to ims-tracker application logs:

~~~
docker logs -f imstrackerdeployment_ims-tracker_1
~~~

or enter the container directly:

~~~
docker exec -it imstrackerdeployment_ims-tracker_1 bash
~~~