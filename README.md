# Dockerfiles_OOpenMS
Dockerfiles for open search applications in the openms framework

All docker container apart from openms_db_search are available in dockerhub in the tillenglert namespace.

https://hub.docker.com/u/tillenglert

If the images are build on your own, you can either tag them with
tillenglert/oopenms_base:latest
tillenglert/oopenms_post_process:latest
tillenglert/oopenms_db_search:latest

The oopenms_base image is based on openms/contrib, which may run into problems when pulling the contrib image from the openms namespace.
If there is an error try building the openms/contrib image and tag it as openms/contrib:latest before building the oopenms_base image

# DB_Search Image

To build the image line 13 needs to be changed in the dockerfile. The image clones a github repository into the image and sets the path accordingly.
As the licensing of MSFragger is to restrictive, the repository I used was private as well as the db_search image on dockerhub. Therefore, I used login tokens for github to access the repository while building the image.
The line looked something like this:

git clone https://tillenglert:LOGINTOKEN@github.com/tillenglert/MSFragger /thirdparty/MSFragger && \


Of course this can be solved with a local repository, then the line can be changed accordingly and the files need to be copied to the thirdparty directory.

# QuantMS changes and execution

The QuantMS workflow will pull all images from my namespace (https://hub.docker.com/u/tillenglert) apart from the db_search image.
Therefore this needs to be build prior to execution.
If the image is tagged something else than tillenglert/oopenms_db_search:latest the conatinername needs to be changed in the MSFraggerAdapter process.

The corresponding file is found at:
https://github.com/tillenglert/quantms/blob/feature/Open_Search_MSFragger/modules/local/openms/thirdparty/searchenginemsfragger/main.nf

Line 5 needs to be changed.

The executable path parameter of the MSFraggerAdapter is set to "". Therefore it will search for MSFragger in the PATH environmental variable.
If the path of the Executable is somewhere else, you can also change this parameter according to your own path. 