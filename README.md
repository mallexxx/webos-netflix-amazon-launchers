# Replace Netflix & Amazon Buttons Apps on WebOS Magic Remote

This repository contains two dummy WebOS apps with `netflix` and `amazon` app IDs. They only serve to launch another application, specified by its app ID. The apps do not have a starting page; they simply launch the specified application immediately.

## Pre-requisites

1. LG (Konka) WebOS TV.
2. An operating system supported by the WebOS SDK (e.g. Ubuntu, Windows 10, macOS).
3. Node.js installed (required for the `ares` toolset).
4. WebOS SDK installed.

## Installing Development Tools

Follow the official instructions to install the WebOS SDK:

[WebOS SDK Installation Guide](http://webostv.developer.lge.com/sdk/installation/)

## Modifying the Launcher Apps

The apps are set to launch the Kinopoisk app (`com.685631.3411` app ID) for the Netflix button and [YouTube AdFree](https://repo.webosbrew.org/apps/youtube.leanback.v4) (`youtube.leanback.v4` app ID) for the Amazon button.

To launch other apps of your choice, open the `index.html` files in your favorite text editor and find the following lines:

```javascript
var params = JSON.stringify({
  "id": "youtube.leanback.v4"  // YouTube No Ads
});
```

Replace `"youtube.leanback.v4"` (or `"com.685631.3411"`) with the app ID of the application you want to launch.

## Finding the Bundle ID of the App to Launch

You can find the bundle IDs of available apps on LG's homebrew channels. Refer to the list of repositories provided [here](https://forum.xda-developers.com/t/webos-homebrew-channel-other-repos-for-testing.4401105/).

Once you have found an app you want to launch, download its `.ipk` file by appending the filename to the URL of the listing server, then extract the `.ipk` file and find the bundle ID in the `appinfo.json` file.

## Building and Installing the Apps

Use the `ares` command-line tools to package and install your app:

- Remove the Netflix and Amazon apps from your TV.

```bash
    # navigate to the launcher app directory
    cd netflix-launcher

    # build the package
    ares-package .

    # install the Netflix Launcher app
    ares-install --device your_tv_name ./netflix_1.0.0_all.ipk
```

- Repeat the above steps for the `amazon-launcher` directory to install the Amazon button app.
- Note: The `ares-install` command requires a connection to your WebOS TV. Please refer to the [WebOS SDK instructions](http://webostv.developer.lge.com/sdk/tools/using-webos-tv-cli/) for details on how to set this up.

## Troubleshooting

- If you keep getting the `ares-install ERR! [com.webos.appInstallService failure]: luna-send command failed <ipk verified failed>` error, press the Amazon button on your Magic Remote. It will open the Store app and start installing the Amazon app. As soon as the 'Install' button changes to 'Cancel', press the 'Cancel' button and run `ares-install` again. It should install it.
- If you encounter any other problems, please refer to the [WebOS developer documentation](http://webostv.developer.lge.com/sdk/docs/) and ensure that your development environment is correctly set up.
