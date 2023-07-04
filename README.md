# devnet quick run scripts for lighthouse + geth

## General information
- All the config files, `genesis.ssz` and other variables needed for the testnet are placed under `custom_config_data`.


## Instructions to join testnet
1. Clone this repository
2. Ensure `docker` and `docker-compose` is installed: `docker-compose --version` and `docker --version`
3. Create the required directories for persistent data with `mkdir -p execution_data beacon_data`
4. Optional: Copy the keys sent by pari, place them in the root of the folder, leave the name of the folder the same (`validator_keys`).
Please reconfirm that the `validator_keys` folder contains a `secrets`, `validators` folders and a `pubkey.json` file. 
5. Find your IP address(public IP) and add it to the `<devnet-name>.vars` file file, this is just to ensure easy peering
   5.1 `curl ifconfig.me` or visit https://whatismyipaddress.com  
   5.2 Replace IP in config file with your own IP address: https://i.imgur.com/xnNqN6h.png
6. Note: If you have an M1 mac, run `export DOCKER_DEFAULT_PLATFORM=linux/amd64` otherwise the images will not be downloaded
7. Run your chosen execution engine, e.g: `docker-compose --env-file <devnet-name>.vars -f docker-compose.geth.yml up -d`
8. Run your chosen consensus engine, e.g: `docker-compose --env-file <devnet-name>.vars -f docker-compose.lighthouse.yml up -d`
9. Check your logs to confirm that they are up and syncing, e.g `docker logs lighthouse_beacon -f --tail=20`
10. To stop the clients, run `docker-compose -f <insert file name you used earlier here> down`
