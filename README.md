# ClouDNS-Updater
ClouDNS updater script is able to be run either as generic Python 3 script or as Docker container. 

### Note: .env file format to Docker variables
When this app runs out of a container it uses an .env file to load config. The file format is as follows:

```
export URL_CDNS = 'https://ipv4.cloudns.net/api/dynamicURL/?q=..........'
export URL_IPIO = 'https://ipinfo.io/json'
export LOG_FILE = 'iplog.txt'
export HOSTNAME = 'put.yourhostname.here'
export SLEEPTIME = 600
```
____Note:____ In order to get your own __URL_CDNS__ you must follow guidance in ClouDNS KB at https://www.cloudns.net/wiki/article/36/.


## Docker run command
In Docker, the way to export variables is to define them on the ```docker run``` execution, on a execution line similar to this:

```
docker run \
    -d --restart unless-stopped \
    --name cloudns-updater \
    -e URL_CDNS="https://ipv4.cloudns.net/api/dynamicURL/?q=.........." \
    -e URL_IPIO="https://ipinfo.io/json" \
    -e LOG_FILE="iplog.txt" \
    -e HOSTNAME="put.yourhostname.here" \
    -e SLEEPTIME=600 \
    ea1het/cloudns-updater:latest 
```

## Docker build command
```
docker build \
    --build-arg VCS_REF=`git rev-parse \
    --short HEAD` \
    --build-arg BUILD_DATE=`date -u +"%Y-%m-%d"` \
    --build-arg VERSION=v1.0 \
    -t ea1het/cloudns-updater:v1.0 .
```
