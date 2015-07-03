# OpenCMISTrial

## References##
* OpenCMIS Server Development Guide

## Setup JAVA DEV ENV##
* https://github.com/draculavlad/JavaDevEnv


## Setup Project with MVN##
```shell
cd ~ && mkdir cmis && cd cmis
mvn archetype:generate \
-DgroupId=jacob.su.cmis \
-DartifactId=server \
-Dversion=1.0-SNAPSHOT \
-Dpackage=jacob.su.cmis.server \
-DprojectPrefix=FileBridge \
-DarchetypeGroupId=org.apache.chemistry.opencmis \
-DarchetypeArtifactId=chemistry-opencmis-server-archetype \
-DarchetypeVersion=1.0.0-SNAPSHOT \
-DinteractiveMode=false
```
