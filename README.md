# Leaderboard HUD

A Fabric mod for Minecraft Java 26.2 that draws a small leaderboard-style
box in the top-left corner of your screen (username, money, stars, kills,
deaths, playtime) and opens an in-game editor when you press **X**.

## Before you build: please read this

Minecraft 26.2 is very new, and Fabric's whole API surface changed a lot
in 26.x (official Mojang mappings by default, renamed classes like
`GuiGraphicsExtractor` and `Identifier`, `GuiGraphics` -> new HUD layer
system, Java 25 requirement, etc). This code was written against the
current Fabric docs and the `fabric-example-mod` repo's `26.2` branch,
but I can't actually compile it here to double-check it. If your IDE
flags an import it can't resolve, it's almost always one of these two
fixes:

- Let IntelliJ IDEA auto-import - it usually finds the moved/renamed
  class for you (Alt+Enter on the red underline).
- Bump `fabric_version` in `gradle.properties` to whatever's newest at
  <https://modrinth.com/mod/fabric-api/versions> for 26.2 - class
  locations inside Fabric API have moved around a few times this year.

## What you need installed

- **Java 25** (the JDK, not just the JRE) - 26.2 requires it.
- **IntelliJ IDEA** (Community is fine) - easiest way to get Gradle set
  up automatically.

## Building

1. Unzip this folder somewhere with no spaces or OneDrive sync (e.g.
   `C:\Projects\leaderboard-hud` or `~/projects/leaderboard-hud`).
2. **Generate the Gradle wrapper jar.** I couldn't include the binary
   `gradle-wrapper.jar` file in this zip, so do one of:
   - Open the folder in IntelliJ IDEA and click "Import Gradle
     Project" when prompted - it'll fetch Gradle for you automatically
     and you can skip step 3 below, **or**
   - If you already have Gradle installed anywhere, run this once
     inside the project folder: `gradle wrapper --gradle-version 9.4`
3. Once Gradle has synced, run:
   - Windows: `gradlew.bat build`
   - macOS/Linux: `./gradlew build`
4. Your compiled mod jar will be at
   `build/libs/leaderboard-hud-1.0.0.jar`.

## Installing

1. Install [Fabric Loader](https://fabricmc.net/use/) for Minecraft
   26.2.
2. Download **Fabric API** for 26.2 from
   [Modrinth](https://modrinth.com/mod/fabric-api) or
   [CurseForge](https://www.curseforge.com/minecraft/mc-mods/fabric-api)
   and drop it in your `mods` folder - this mod depends on it.
3. Drop `leaderboard-hud-1.0.0.jar` in the same `mods` folder.
4. Launch the game with the Fabric profile.

## Using it in-game

- The leaderboard box appears automatically in the top-left corner.
- Press **X** to open the editor and change any of the six values
  (Username, Money, Stars, Kills, Deaths, Playtime) - they accept any
  text, so you can type things like `5B`, `118K`, `107d 3h` exactly
  like the values shown on the box.
- Click **Save** to apply, or **Cancel** to back out.
- You can rebind the key in Options > Controls > Key Binds >
  "Leaderboard HUD".

## Known limitations

- Values reset to the defaults (username "Claude") every time you
  restart the game - they're only kept in memory, not saved to a file.
  If you want them to persist across restarts, the values live in
  `LeaderboardData.java` - the natural next step would be to write
  that class out to a JSON file in `.minecraft/config/` on save and
  read it back in `onInitializeClient()`. Happy to add that if you
  want it.
- The numbers are cosmetic only - nothing here actually tracks real
  kills/deaths/playtime from the game; you type in whatever you want.
