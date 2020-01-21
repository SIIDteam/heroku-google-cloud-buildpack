# heroku google cloud buildpack

This buildpack installs a pinned version of the Google Cloud SDK. During install, it generates a ```google-credentials.json``` file in the build directory, and generates a ```heroku-google-cloud.sh``` script in ```.profile.d``` which activates the Google service account with this credentials file upon server startup.


## Credentials

This script generates a credentials file using the following environment variables (set in Settings > Config Vars). If they're not present, the Google Cloud SDK will be installed, but this buildpack won't generate the credentials file or set the SDK to auth on server startup:

* ```GOOGLE_TYPE```
* ```GOOGLE_PROJECT_ID```
* ```GOOGLE_PRIVATE_KEY_ID```
* ```GOOGLE_PRIVATE_KEY```
* ```GOOGLE_CLIENT_EMAIL```
* ```GOOGLE_CLIENT_ID```
* ```GOOGLE_AUTH_URI```
* ```GOOGLE_TOKEN_URI```
* ```GOOGLE_AUTH_PROVIDER_CERT```
* ```GOOGLE_CLIENT_CERT```

## GOOGLE_APPLICATION_CREDENTIALS

You will also want to set the config var of 
```GOOGLE_APPLICATION_CREDENTIALS``` to ```google-credentials.json```
In the Settings > Config Vars of your Heroku Project

## Installation
From the command line enter these two commands:
```heroku buildpacks:set https://github.com/dhsearl/heroku-google-cloud-buildpack.git -a <APP_NAME_HERE>```
```heroku buildpacks:add --index 1 heroku/nodejs```
First we set the build pack to the heroku-google-cloud-buildpack, then we add nodejs as the first buildpack (pushing the other to the second place)

## Troubleshooting

This script downloads the most recent version of Google Cloud SDK as of January 2020.  If you are experiencing any issues please replace the link and filename with the most recent version.  

This script also has verbose mode turned on for troubleshooting purposes.  You can change this in the script.
Be sure you've set the Google Application Credentials
