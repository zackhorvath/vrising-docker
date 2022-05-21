# Unofficial VRising Docker Container
This is an unofficial VRising container for running servers on Linux. This is a forked version from the [original](https://github.com/Googlrr/V-Rising-Docker-Linux) to make a little more portable. It uses Wine for running the server, so there is going to be some weird file mapping at play.

## Configuration

According to the [official guide](https://github.com/StunlockStudios/vrising-dedicated-server-instructions) there is a default set of configurations, and then an override folder which lives at `/root/.wine/drive_c/users/root/AppData/LocalLow/Stunlock Studios/VRisingServer/Settings/` in this container.

If you map a local directory (`/vrising/settings` in my examples) to the override directory above, you can put game setting overrides in there which are applied every time the container is restarted.

Check out `./default/` in this repo for examples of full config files, or check out `./settings/` for a smaller set that I use. You'll want to make sure these exist in `/vrising/settings` or wherever you put your game configs.


## Deployment w/ docker-compose
This is a quick deployment meant to get you up and running with minimal BS:

1. Create your host's game settings folder:
    ```
    export SETTINGS=/vrising/settings
    export SAVES=/vrising/saves
    mkdir $SETTINGS
    mkdir $SAVES
    ```
2. Copy configs to this folder and modify as neccessary:
    ```
    wget https://raw.githubusercontent.com/zackhorvath/vrising-docker/main/settings/ServerGameSettings.json -o $SETTINGS/ServerGameSettings.json
    wget https://raw.githubusercontent.com/zackhorvath/vrising-docker/main/settings/ServerHostSettings.json -o $SETTINGS/ServerHostSettings.json
    ```
3. Modify `docker-compose.yml` as neccessary, ensuring the volume mapping matches the directory you just created.
4. Launch docker-compose with `docker-compose up -d`

