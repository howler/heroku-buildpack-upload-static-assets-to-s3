# Purpose

Uploads static assets to S3 when building Heroku apps.

Requires the NodeJS buildpack to be installed. `https://github.com/heroku/heroku-buildpack-nodejs`


# Setting Mandatory Environment Variables for Build

Important all environmental variables must be set. 
There are no defaults the values below are the suggested values.

```
AWS_ACCESS_KEY_ID=<aws access key id>
AWS_SECRET_ACCESS_KEY=<aws secret access key>
AWS_DEFAULT_REGION=<aws-region>
AWS_STATIC_BUCKET_NAME=<s3-bucket-name>
# prefix to include in path
AWS_STATIC_PREFIX=static
# The directory to upload to S3 (uploads the content of the directory)
AWS_STATIC_SOURCE_DIRECTORY=public
# Remove AWS_STATIC_SOURCE_DIRECTORY folder after upload is complete
RM_AWS_STATIC_SOURCE_DIRECTORY=true
# Remove nodes_modules folder after upload is complete
RM_NODE_MODULES=true
```

# Exported Environment Variables to Runtime

```sh
STATIC_SERVER=<AWS_STATIC_BUCKET_NAME>.s3.amazonaws.com
STATIC_PATH=/<AWS_STATIC_PREFIX>/<HEROKU_APP_NAME>/<HEROKU_RELEASE_VERSION>/<guid>
```

These variables can be overriden with config vars as expected

```
heroku config:set STATIC_SERVER=your.cdn.host
```

To return to the default value just unset the config vars

```
heroku config:unset STATIC_SERVER
```
