# AuthorizedMC Launcher

The official launcher for **AuthorizedMC Client**, a client-side Fabric mod for Minecraft: Java Edition 1.21.11
made for the [AuthorizedMC](https://authorizedmc.net/) Minecraft network.

## What it does

1. **Signs players in** with their own Microsoft account (Microsoft → Xbox Live → Minecraft Services).
2. **Verifies ownership** of Minecraft: Java Edition through Minecraft Services before anything launches.
   Accounts that don't own the game cannot play.
3. **Downloads the game from official sources only**: the client, libraries and assets from Mojang's
   servers, and the Java runtime from Mojang's runtime manifest. Every file is checked against its SHA-1 hash.
   No Minecraft files are redistributed by this project.
4. **Installs Fabric Loader** (meta.fabricmc.net), **Fabric API** (Modrinth) and the **AuthorizedMC Client** mod.
5. **Launches the game** in its own folder (`%APPDATA%\.authorizedmc`), separate from the official launcher.

Account tokens are stored only on the player's computer and are encrypted with the operating system's
keychain. The launcher has no backend server and sends no analytics.

- Website: https://authorizedmc.net/
- [Privacy Policy](PRIVACY.md) · [EULA](EULA.md)
- Not affiliated with Mojang or Microsoft.

---

## For the developer

### Run it (Windows, Node.js 18+)
```
cd authorizedmc-launcher
npm install
npm start
```

### Test the download engine before sign-in is approved
Settings → **Use a local client jar** → pick your `authorizedmc-hud-1.7.0.jar`, then
Settings → **Install / Repair**. It downloads and verifies Minecraft, Java, Fabric and the mods
without needing an account.

### Build the Windows installer
```
npm run dist
```
The installer appears in `dist\`.

### Turn on Microsoft sign-in
When Mojang approves the app registration, paste the Application (client) ID into
`src/core/config.js` → `AZURE_CLIENT_ID`, then rebuild.

### Publishing client updates
The launcher downloads the client from
`https://github.com/AirThru/AuthorizedMC-Client/releases/latest/download/authorizedmc-client.jar`.
Create that repository, then for every client version publish a GitHub Release with the jar attached
as **authorizedmc-client.jar**. Players get it automatically the next time they press Play.
