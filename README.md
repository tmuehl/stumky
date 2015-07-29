# Stumky (The Stups Monkey Scripts)

Some monkey helper scripts around the teamup of docker and senza and the rest of the stups ecosystem. It makes daily life under the cloud and top of the docker vessel easier.

Within your project folder you build and push a new version docker image with ```stumky-docker-build```. Accordingly, you create a new version of your cloud formation template with ```stumky-senza-build```. Both scripts will remember your application name and definition file such it's not necessary to refrain them everytime. Furthermore they increment and handle the version numbers automatically.

The ```docker-build``` script will build SNAPSHOT versions until you specify the ```--release``` flag. 

## Install

Clone the repository into a local folder and add it to your path. E.g. add the folling line to your .profile:

    echo 'PATH="'`pwd`'$PATH"' >> ~/.profile

You also have to set a PIERONE_APP_PREFIX environment variable that is used to generate the tag for the docker images:

    export PIERONE_APP_PREFIX=pierone.example.com/myteam/

## Tools

### stumky-docker-build

Builds a new docker image and pushes the image to pierone. By default, it builds a SNAPSHOT of the current version. With the ```--release``` flag, it increases the version number.

    stumky-docker-build [OPTIONS]

Possible options:

```
OPTIONS can be:
--help, -h     print help and exit.
--no-push, -n  dry run. dont push to pierone.
--release, -r  build a release version instead of a snapshot version
```

### stumky-senza-build

Builds a new cloud formation template with senza. It uses the latest known docker image, so ```stumky-docker-build``` must have been called at least once before.

    stumky-senza-build [OPTIONSS]

Possible options:

```
--events    show the cloud formation event log immediately after deployment
```

### stumky-scalyr-log

With the stumky-scalyr-log frontend you can easily see the last 5000 lines of the logfile of your application on scalyr. The syntax is:

    stumky-scalyr-log <FILENAME>

For example:

    stumky-scalyr-log application.log | less

Unfortunately, we are limited to 5000 lines by scalyr.

