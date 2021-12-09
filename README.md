# Amazon AppStore Deployment Github Action

GitHub Actions to deploy an app (.apk) to Amazon AppStore. All the steps on this action were created based on the [Amazon AppStore -> API Task Flows](https://developer.amazon.com/docs/app-submission-api/flows.html)

## Prerequisites

The app must be live on Amazon AppStore. If not you will receive the error `Cannot create a new 'edit' for the app in it's current state.` when the action tries to create the Edit.

## Inputs

### `client-id`

**Required** The client ID of the Amazon AppStore application.

### `client-secret`

**Required** The client secret of the Amazon AppStore application.

### `app-id`

**Required** The ID of the Amazon AppStore application.

### `apk-file`

**Required** The path to the APK file to deploy.

## Sample usage

```yml
name: Build & upload to Firebase App Distribution 

on: [push]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - name: set up JDK 1.8
      uses: actions/setup-java@v1
      with:
        java-version: 1.8
    - name: build release 
      run: ./gradlew assembleRelease
    - name: Upload to the Amazon AppStore
      uses: ALJAZEERAPLUS/amazon-appstore-action@v1
      with:
        client-id: ${{secrets.AMAZON_APPSTORE_CLIENT_ID}}
        client-secret: ${{secrets.AMAZON_APPSTORE_CLIENT_SECRET}}
        app-id: ${{ secrets.AMAZON_APPSTORE_APP_ID }}
        apk-file: app/build/outputs/apk/release/app-release.apk
```

## :gear: Inputs

| Name          | Description                                           | Default | Required |
| ------------- | ----------------------------------------------------- | :-----: | :------: |
| client-id     | The client ID of the Amazon AppStore application.     |         |   True   |
| client-secret | The client secret of the Amazon AppStore application. |         |   True   |
| app-id        | The ID of the Amazon AppStore application.            |         |   True   |
| apk-file      | The path to the APK file to deploy.                   |         |   True   |

## :thought_balloon: Support

If you find our work useful, but for some reason there is something missing, please raise a pull request to us review it!
