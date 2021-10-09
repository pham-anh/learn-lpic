---
title: git error when deploying Google App Engine Flexible with sample code
date: 2021-10-06
tags:
- gae
- AppEngine
categories:
- Google Cloud Platform
---

## Deploy Hello World app

For setup, follow this guidance here: https://cloud.google.com/appengine/docs/flexible/go/quickstart

* If we don't do these setup steps, an error `exec: "gcc": executable file not found in $PATH` may occur when running `gcloud app deploy`

My environment: 

```
$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
$ git version
git version 1.8.3.1
$ go version
go version go1.15.14 linux/amd64
```

Download go sample Hello World app and try running it locally.

```
$ git clone github.com/GoogleCloudPlatform/golang-samples
$ cd golang-samples/appengine_flexible/helloworld
# Run it locally
$ go run *.go
```

There was an error: `fatal: git fetch-pack: expected shallow list`
```
go: cloud.google.com/go/bigtable@v1.4.0 requires
        google.golang.org/api@v0.28.0 requires
        honnef.co/go/tools@v0.0.1-2020.1.3 requires
        golang.org/x/mod@v0.0.0-20190513183733-4bf6d317e70e: invalid version: git fetch --unshallow -f origin in /xxx/go/pkg/mod/cache/vcs/13df7481b5cc3358460b717a6142fe8dbaae7652e5d05689849f419ffd40ac12: exit status 128:
        fatal: git fetch-pack: expected shallow list
```

### How to solve `fatal: git fetch-pack: expected shallow list` ?

The causes seems to be that git and go versions are too old. So I upgrade them to newer versions.

#### Upgrade git to 2.22

```
$ sudo yum erase git
$ sudo yum install https://repo.ius.io/ius-release-el7.rpm
$ sudo yum install git222
$ git version
git version 2.22.5
```

#### Upgrade go to 1.17

```
$ curl -O -L https://golang.org/dl/go1.17.1.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.17.1.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin # or add it into .bash_profile
$ go version
go version go1.17.1 linux/amd64
```

## Deploy Hello World app (cnt)

Rerun the app locally.

```
$ go run *.go
2021/10/06 21:25:23 Listening on port 8080
```

This time it was successful.

Now deploy it to App Engine.

```
$ gcloud app deploy
Services to deploy:

descriptor:                  [/xxx//golang-samples/appengine_flexible/helloworld/app.yaml]
source:                      [/xxx//golang-samples/appengine_flexible/helloworld]
target project:              [xxx]
target service:              [default]
target version:              [20211006t212756]
target url:                  [https://xxx.et.r.appspot.com]
target service account:      [App Engine default service account]


Do you want to continue (Y/n)?  Y

Beginning deployment of service [default]...
Building and pushing image for service [default]
Started cloud build [e9dcb100-372e-4986-be99-e1440bdf97b6].
To see logs in the Cloud Console: https://console.cloud.google.com/cloud-build/builds/e9dcb100-372e-4986-be99-e1440bdf97b6?project=xxx
----------------------------------------------------------------------- REMOTE BUILD OUTPUT ------------------------------------------------------------------------
starting build "e9dcb100-372e-4986-be99-e1440bdf97b6"

FETCHSOURCE
Fetching storage object: gs://staging.xxx.appspot.com/asia.gcr.io/xxx/appengine/default.20211006t212756:latest#1633555680352376
Copying gs://staging.xxx.appspot.com/asia.gcr.io/xxx/appengine/default.20211006t212756:latest#1633555680352376...
- [1 files][  1.2 KiB/  1.2 KiB]                                                
Operation completed over 1 objects/1.2 KiB.                                      
BUILD
Starting Step #0
Step #0: Pulling image: gcr.io/gcp-runtimes/go1-builder@sha256:408a098788ef4cdeec452821946b986ef82ce5ebceecbdf748ffecf329765bce
Step #0: gcr.io/gcp-runtimes/go1-builder@sha256:408a098788ef4cdeec452821946b986ef82ce5ebceecbdf748ffecf329765bce: Pulling from gcp-runtimes/go1-builder
Step #0: 6c5b97b864a6: Already exists
Step #0: 8ca77d5ce166: Pulling fs layer
Step #0: 3c2cba919283: Pulling fs layer
Step #0: f51d1e50dfed: Pulling fs layer
Step #0: 93d357f3c912: Pulling fs layer
Step #0: 38c250bc4956: Pulling fs layer
Step #0: 194752cda0cd: Pulling fs layer
Step #0: 7e8b9278b356: Pulling fs layer
Step #0: c0baf66a8378: Pulling fs layer
Step #0: 93d357f3c912: Waiting
Step #0: 38c250bc4956: Waiting
Step #0: 194752cda0cd: Waiting
Step #0: 7e8b9278b356: Waiting
Step #0: c0baf66a8378: Waiting
Step #0: 3c2cba919283: Verifying Checksum
Step #0: 3c2cba919283: Download complete
Step #0: 93d357f3c912: Verifying Checksum
Step #0: 93d357f3c912: Download complete
Step #0: 8ca77d5ce166: Verifying Checksum
Step #0: 8ca77d5ce166: Download complete
Step #0: 38c250bc4956: Download complete
Step #0: 7e8b9278b356: Verifying Checksum
Step #0: 7e8b9278b356: Download complete
Step #0: c0baf66a8378: Verifying Checksum
Step #0: c0baf66a8378: Download complete
Step #0: f51d1e50dfed: Verifying Checksum
Step #0: f51d1e50dfed: Download complete
Step #0: 194752cda0cd: Verifying Checksum
Step #0: 194752cda0cd: Download complete
Step #0: 8ca77d5ce166: Pull complete
Step #0: 3c2cba919283: Pull complete
Step #0: f51d1e50dfed: Pull complete
Step #0: 93d357f3c912: Pull complete
Step #0: 38c250bc4956: Pull complete
Step #0: 194752cda0cd: Pull complete
Step #0: 7e8b9278b356: Pull complete
Step #0: c0baf66a8378: Pull complete
Step #0: Digest: sha256:408a098788ef4cdeec452821946b986ef82ce5ebceecbdf748ffecf329765bce
Step #0: Status: Downloaded newer image for gcr.io/gcp-runtimes/go1-builder@sha256:408a098788ef4cdeec452821946b986ef82ce5ebceecbdf748ffecf329765bce
Step #0: gcr.io/gcp-runtimes/go1-builder@sha256:408a098788ef4cdeec452821946b986ef82ce5ebceecbdf748ffecf329765bce
Finished Step #0
Starting Step #1
Step #1: Already have image (with digest): gcr.io/kaniko-project/executor@sha256:b9eec410fa32cd77cdb7685c70f86a96debb8b087e77e63d7fe37eaadb178709
Step #1: INFO[0000] Retrieving image manifest gcr.io/distroless/base@sha256:1a80a34cb3d7c4326191047976e4161741aef22c351932b55e32b72ce8827c27 
Step #1: INFO[0000] Retrieving image gcr.io/distroless/base@sha256:1a80a34cb3d7c4326191047976e4161741aef22c351932b55e32b72ce8827c27 
Step #1: INFO[0000] Built cross stage deps: map[]                
Step #1: INFO[0000] Retrieving image manifest gcr.io/distroless/base@sha256:1a80a34cb3d7c4326191047976e4161741aef22c351932b55e32b72ce8827c27 
Step #1: INFO[0000] Retrieving image gcr.io/distroless/base@sha256:1a80a34cb3d7c4326191047976e4161741aef22c351932b55e32b72ce8827c27
Step #1: INFO[0001] Executing 0 build triggers                   
Step #1: INFO[0001] Unpacking rootfs as cmd COPY bin/ /usr/local/bin/ requires it. 
Step #1: INFO[0002] LABEL build_tag="1.11.13-20211004_2020"      
Step #1: INFO[0002] Applying label build_tag=1.11.13-20211004_2020 
Step #1: INFO[0002] LABEL go_version="1.11.13"                   
Step #1: INFO[0002] Applying label go_version=1.11.13            
Step #1: INFO[0002] COPY bin/ /usr/local/bin/                    
Step #1: INFO[0002] Taking snapshot of files...                  
Step #1: INFO[0002] COPY app/ /app/                              
Step #1: INFO[0002] Taking snapshot of files...                  
Step #1: INFO[0002] WORKDIR /app                                 
Step #1: INFO[0002] cmd: workdir                                 
Step #1: INFO[0002] Changed working directory to /app            
Step #1: INFO[0002] No files changed in this command, skipping snapshotting. 
Step #1: INFO[0002] ENTRYPOINT ["/usr/local/bin/app"]
Finished Step #1
PUSH
DONE
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
Updating service [default] (this may take several minutes)...done.                                                                                                 
Setting traffic split for service [default]...done.                                                                                                                
Deployed service [default] to [https://xxx.et.r.appspot.com]

You can stream logs from the command line by running:
  $ gcloud app logs tail -s default

To view your application in the web browser run:
  $ gcloud app browse

```

The deployment was successful. Go to Google Cloud Console and we can see the new version of the app.

![App Engine Flexible](../img/20211007-deploy-gae-flex.png)


## References

https://github.com/golang/go/issues/38373

