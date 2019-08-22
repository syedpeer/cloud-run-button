# Readme

[![Run on Google Cloud](https://storage.googleapis.com/cloudrun/button.svg)](https://console.cloud.google.com/cloudshell/editor?shellonly=true&cloudshell_image=gcr.io/cloudrun/button&cloudshell_git_repo=https://github.com/sanderhahn/cloud-run-button)

Deploys Sapper without a Dockerfile on Google Cloud Run by using [Buildpacks.io](https://buildpacks.io/).
Sapper uses an `npm build` command that is now being triggered using the `postinstall` script.

Google uses the Heroku buildpacks (`heroku/buildpacks`) to build an image which is pretty heavy at 770MB.
The Cloud Foundry buildpacks (`cloudfoundry/cnb:bionic`) build an image that much smaller at 170MB.

You can emulate the build process that Google performs locally by installing [pack](https://github.com/buildpack/pack):

```bash
# shows available builders
pack suggest-builders
# inspect it
pack inspect-builder heroku/buildpacks
# pick the one google uses
pack set-default-builder heroku/buildpacks
# perform a build
pack build cloud-run-button

# start the image
docker run --name cloud-run-button -p 3000:3000 -d cloud-run-button
# stop the image
docker stop cloud-run-button
# remove the image
docker rm cloud-run-button

# clean up build cache
docker volume prune -f
```
