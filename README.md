# signal-bridge

This is a Matrix bridge for Signal, the secure messenger app by Open Whisper Systems.

It works through a dirty port of the [Signal Chrome App](https://github.com/WhisperSystems/Signal-Desktop) to Node.js, which serves as the client. You can find that here: https://github.com/matrix-hacks/node-signal-client

## features

- [x] Linking as a second device
- [x] Signal to Matrix direct text message
- [x] Matrix to Signal direct text message
- [x] Signal to Matrix direct image attachment message
- [ ] Matrix to Signal direct image attachment message
- [ ] group messaging
- [ ] read receipts
- [ ] contact list syncing

## requirements

You need an iOS and Android phone with an existing Signal account that you are willing to link with the Signal client in this bridge.

## installation

clone this repo

cd into the directory

run `npm install`

## register/link with your signal mobile app

Before configuring the bridge with Matrix, **you need to setup the Signal link with your phone**.
Open up your Signal app and go to Settings and then Linked Devices.
You should see your camera preview open up.

In the terminal, run `npm run link` and you should soon see a giant QR code. Scan that with Signal.

If you get an error, restart the node process so that you can try with a different QR (it may have expired).

If you ever need to unlink it and cleanup the data and keys, run `npm run clean`.
Make sure to delete the linked device from the Signal mobile app as well.

## configure

Copy `config.sample.json` to `config.json` and update it to match your setup

## register the app service

Generate an `signal-registration.yaml` file with `node index.js -r -u "http://your-bridge-server:8090"`

Note: The 'registration' setting in the config.json needs to set to the path of this file. By default, it already is.

Copy this `signal-registration.yaml` file to your home server, then edit it, setting its url to point to your bridge server. e.g. `url: 'http://your-bridge-server.example.org:8090'`

Edit your homeserver.yaml file and update the `app_service_config_files` with the path to the `signal-registration.yaml` file.

Launch the bridge with ```node index.js```.

Restart your HS.

# TODO
* Be able to originate conversations from the Matrix side.
