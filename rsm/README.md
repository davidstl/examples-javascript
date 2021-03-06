# Room Server Manager #

This Room Server Manager (RSM) is also running it's RoomServers (RS) inside the same instance. We have done this for simplicity.


The game the system hosts is **War Stone**, another brainCloud RTT example.


New test games can be added to the RSM example, in RoomServerManager.js:

```
switch (room.appId)
{
    case "22819":
        roomServer = new TurnBasedRoomServer(room, "WarStone");
        break;

    case "12038":
        roomServer = new TurnBasedRoomServer(room, "YourNewGame");
        break;
        
    default:
        return null;
}
```

`TurnBasedRoomServer` is also re-usable for turn-based games.





# War Stone #
Turned Based card game, built as an example for brainCloud real-time Room Server Manager (RSM) and real-time Matchmaking

![](screenshots/warstone.png)

## Play the game ##
To play the game now, follow this link:
http://ec2-18-219-26-183.us-east-2.compute.amazonaws.com:3000/

> Play against yourself to get into a game fast: Run two browser tabs of the game with separate logins (username/pw). Matchmaking will most likely place you together in the same game.

## How to run your instance ##
You might want to modify this example, for your individual needs and debugging purposes. 

To further familiarize yourself with the system, it is a good idea to try to run your own War Stone project.

### Portal setup ###
We first need to create the application in the brainCloud portal, then upload configuration that defines the settings and rules of the game.
1. Create a new app, call it `War Stone` or your chosen project name.

2. In the **Design / Core App Info / Admin Tools** section of the portal, then **Import Configuration Data** from `portal-configs/configuration-data.bcconfig`.
3. In the **Design / Cloud Code / Web Services** section of the portal, edit the **Base URL** of the **RSM** service. By default, it points to the example RSM instance.
4. Now in the portal, go in the section **Monitoring / Global Entities** and **Bulk Actions / Import from Raw JSON Object file** from `portal-configs/global-entities_raw.json`

### Run the server ###
1. Clone the RSM example from here: https://github.com/getbraincloud/rsm-example
2. Make sure your router allows for TCP ports 9306/9308/9310. If you wish to change the ports, check in the file `server/Scripts/main.js` for `TCP_PORT`, `HTTP_PORT` and `WS_PORT`.

   Don't forget to update the URL for the RSM in the portal.
3. In the file `server/Scripts/S2S.js`, fill in the following information:
   ```
   const APP_ID = "..."; // Fill in the appId
   ```
   AppId in **Design / Core App Info / Application IDs**
   ```
   const SERVER_SECRET = "..."; // Fill in the server secret
   ```
   Server secret in **Design /  Cloud Code / S2S Config / RSM**
4. In the `server/Scripts/RoomServerManager.js`, fill in the following information:

```
    switch (room.appId)
        {
            case "...": // Fill in the appId
                roomServer = new TurnBasedRoomServer(room, "WarStone");
                break;
            default:
                return null;
    }
```
  AppId in **Design / Core App Info / Application IDs**

5. It's a nodejs project. It can be started by calling the following via the cmdline:
   ```
   cd server/
   npm install
   node Scripts/main.js
   ```

### Run the client ###
1. Clone the WarStone example from here: https://github.com/getbraincloud/warstone

2. In the file `src/App.js`, fill in the following in formation:
   ```
   let appId = "..." // Fill in the appId
   let appSecret = "..." // Fill in the appSecret
   ```
   Found in **Design / Core App Info / Application IDs**
3. Install npm modules: `npm install`
4. Run: `npm start`
