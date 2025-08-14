# cleanopsT7_server
A Patch for Call of Duty: Black Ops 3 - Unranked Dedicated Server

## Overview
`cleanopsT7_server` transforms the official Unranked Dedicated Server into a fully functional ranked server, allowing players to gain XP, level up weapons, and unlock content just like on an official server. This patch is for Multiplayer only and includes fixes for several known exploits.
Cryptokey progression is not yet supported with this patch, but I am actively working on a solution to enable it in a future update.

This patch is designed to be inclusive, allowing players who spoof their DLCs to seamlessly join and play on DLC maps. This helps maintain a larger and more active player base on your server.

***Important Note:*** To make your server visible in the `cleanopsT7` server browser and to utilize our custom database for ban management, you must contact us on **Discord** to obtain a unique **API key**. Without this key, your server will only be discoverable through the Black Ops 3 Mod Tools Server Browser. 

## Installation
-   Open your Steam client, navigate to Library, and under the Tools tab,<br>
    find and download **Call of Duty: Black Ops III - Unranked Dedicated Server**.

-   Download the latest release of `faultrep.dll` from the [releases](https://github.com/notnightwolf/cleanopsT7_server/releases) tab.

-   Move the `faultrep.dll` into your server directory<br>
    (usually located in C:\Program Files (x86)\Steam\steamapps\common\Call of Duty Black Ops III\UnrankedServer).

-   Launch the `BlackOps3_UnrankedDedicatedServer.exe` once, wait a few seconds and close it again.

-   After launching the server for the first time, a folder named cleanops will be created in your server directory.<br> 
    Inside this folder, you will find a `config.json` file. Open this file and adjust the settings to suit your servers needs.

-  Launch `BlackOps3_UnrankedDedicatedServer.exe`. Your server is now ready and running with the patch applied.

## Config
The `config.json` file allows you to customize various settings for your `cleanopsT7_server` instance. Here is a breakdown of the available options:
```
{
  "api_key": "",
  "live_steam_server_description": "This is a server",
  "live_steam_server_name": "Test Server",
  "live_steam_server_password": "test",
  "logfile": "2",
  "max_players": "18",
  "net_port": "27017",
  "rcon_password": "",
  "shuffle_playlists": false,
  "sv_playlist": "1",
  "tempban_duration": "60"
}
```
- `api_key`: This is the unique key you receive from us on Discord. It is required to make your server visible inside the `cleanopsT7` server browser and to get access to our ban management database.

- `live_steam_server_description`: The description that will appear in the server browser.

- `live_steam_server_name`: The name of your server that will be visible to other players.

- `live_steam_server_password`: If you want to protect your server with a password, enter it here. Leave it blank for a public server.

- `logfile`: Specifies the logging level. A value of "2" enables logging without buffering.

- `max_players`: The maximum number of players allowed on your server.

- `net_port`: The network port the server will use.

- `rcon_password`: The password for Remote Console (RCON) access, used for server administration.

- `shuffle_playlists`: Set to `true` to enable random playlist selection. This will cause the server to roll a random number for `sv_playlist`, cycling through your available playlists, while the map order within each playlist remains the same. Set to `false` to use the specific `sv_playlist` ID configured in this file.

- `sv_playlist`: The ID of the playlist to be used for the gametype rotation.

- `tempban_duration`: The duration of a temporary bans in minutes.

## Playlists
Playlists are defined in the `playlists.info` file located in the `machinecfg` folder. This file determines the map and game mode rotation for your server. Each playlist is identified by a unique number. The `party_minplayers` rule specifies the minimum number of players required for a match to start.

If you wish to use another gamemode, it must first be added to the `GAMETYPES` section before it can be used in a playlist.

Here is an example of what your `playlists.info` file might look like:
```
///////////////////////////////////////////////////////////////////////////
// SERVER SETTINGS
///////////////////////////////////////////////////////////////////////////
settings

///////////////////////////////////////////////////////////////////////////
// GAMETYPES
///////////////////////////////////////////////////////////////////////////
gametype tdm
script tdm

///////////////////////////////////////////////////////////////////////////
// PLAYLISTS
///////////////////////////////////////////////////////////////////////////

//non-dlc-map-playlist
playlist 1
rule party_minplayers 2
mp_apartments,tdm
mp_biodome,tdm
mp_chinatown,tdm
mp_ethiopia,tdm
mp_havoc,tdm
mp_infection,tdm
mp_metro,tdm
mp_redwood,tdm
mp_sector,tdm
mp_spire,tdm
mp_stronghold,tdm
mp_veiled,tdm
mp_nuketown_x,tdm
mp_redwood_ice,tdm
mp_veiled_heyday,tdm

//dlc-map-playlist
playlist 2
rule party_minplayers 2
mp_apartments,tdm
mp_biodome,tdm
mp_chinatown,tdm
mp_ethiopia,tdm
mp_havoc,tdm
mp_infection,tdm
mp_metro,tdm
mp_redwood,tdm
mp_sector,tdm
mp_spire,tdm
mp_stronghold,tdm
mp_veiled,tdm
mp_nuketown_x,tdm
mp_redwood_ice,tdm
mp_veiled_heyday,tdm
mp_crucible,tdm
mp_skyjacked,tdm
mp_waterpark,tdm
mp_rise,tdm
mp_aerospace,tdm
mp_banzai,tdm
mp_conduit,tdm
mp_kung_fu,tdm
mp_arena,tdm
mp_cryogen,tdm
mp_rome,tdm
mp_shrine,tdm
mp_city,tdm
mp_miniature,tdm
mp_ruins,tdm
mp_western,tdm

// must have a hard return after this line
```
You can choose to use Playlist 1 for non-DLC maps or Playlist 2 for a full rotation including DLC. While you can change the game modes or create new playlists, it's crucial that you **do not change the order of the maps** in a playlist. This is because the server's voting system relies on this specific order to function correctly.

The `sv_playlist` setting in your `config.json` file specifies which playlist the server should use. If `shuffle_playlists` is set to `true`, the server will randomly choose from all the playlists defined in your `playlists.info` file. If it's set to `false`, the server will always use the playlist specified by the `sv_playlist` ID.

## Port Forwarding
For players to connect to your server from outside your local network, you must configure port forwarding on your router. This process directs incoming traffic on specific ports to your server's local IP address.

**Required Ports:**

The following ports need to be forwarded for the server to be fully functional and visible to players.

- **TCP**: `3074`, `27014-27050`

- **UDP**: `3074`, `4380`, `27000-27031`, `27036`

