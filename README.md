# VPet (VitalPet): a Digimon farm for your phone and your watch

> **Built on [VB Helper](https://github.com/nacabaro/vbhelper) by nacabaro and [VitalWear](https://github.com/cfogrady/VitalWear) by cfogrady**, with the work of many contributors. See [CREDITS.md](CREDITS.md).

A free, non-profit fan project. Two apps and a server:

| Piece | What it is | File |
|---|---|---|
| **VPetFarm** | Android phone app: your farms, your Digimon, your account, online battles | `VPetFarm-telefono.apk` |
| **VPetWear** | Wear OS watch app: your Digimon walks, trains and fights with you | `VPetWear-reloj.apk` |
| **Server** | Keeps your progress and referees the battles (already online, nothing to install) | none |

Your progress lives on the server: if you change phone or watch, your Digimon stay on your account. The apps are in English.

The installers are in [Releases](../../releases/latest). **You only install by hand the first time**: after that both apps update themselves (see below).

**Website and guides:** https://vpet.utopicflow.com

> **Heads up:** for now the server runs on a home NAS. If the power or the internet goes out at my house, the game can be offline for a while or lose connection. News and outages are posted on the Discord.

## Support the project

The game is free and always will be. If you would like to help make the server more reliable (a battery backup, a backup internet connection, solar panels with a battery and, in the end, satellite internet), you can leave an optional donation at **https://buymeacoffee.com/vitalpet**. Donations give no gameplay advantages.

## Features

### Phone (VPetFarm)
- **Farms:** raise your Digimon on one or more farms. Build training objects, buy boosts and items with coins.
- **Six stats:** HP, MP, ATK, DEF, SPD and BRN, plus levels, mood, personality and the blue and white bonus points.
- **Walking matters:** your steps level up your tamer, your farms and your team.
- **Evolutions follow the cards:** each Digimon evolves by the rules of its DIM/BEM card (time, vitals, trophies, fights, win rate and adventure missions). You can also take a Digimon back one stage.
- **Online battles:** an attack team and a defence team of 3. Give orders each round (attack, special, guard) and climb the monthly rankings. Defence teams fight for you while you are away.
- **Scans:** every Digimon of a card you fight fills that card's scan. At 100% you can make the card's Baby I; anything above 100% adds bonus stat points.
- **Card adventure:** each card has missions. Walk the steps, beat the boss, earn coins and experience, and unlock the evolutions that ask for the adventure.
- **Dex and cards:** import your own DIM/BEM cards and see your collection, scans and adventure progress per card.
- **Custom cards:** upload a card on the website, sign in with Discord, and once approved its Digimon join the game for everybody.

### Watch (VPetWear)
- Send a Digimon from your farm to your Wear OS watch.
- Every step is a chance to meet wild Digimon of its stage. You fight them, they give experience and your scans grow.
- Training exercises (crunch, punch, dash, squat), the card's adventure missions and evolution by the card's rules.
- Everything is reported to your farm.

### With your Vital Bracelet
- Read your bracelet over NFC and bring its Digimon to the farm with its vitals, trophies, fights, age and time to evolve.
- Send it back whenever you want. What it earned on the farm (levels, training, blue and white points) is kept for when it returns.
- The card adventure missions are kept the same between the bracelet, the watch and the farm.

## Installation

### Phone (VPetFarm)
1. Download `VPetFarm-telefono.apk` from [Releases](../../releases/latest) on the phone and open it.
2. Android asks for permission to install apps from that source: accept.
3. If you had an older version signed with another key (the original VBHelper or a test build), uninstall it first.

### Watch (VPetWear)
The watch has no store: it is installed from a computer with `adb`.

1. On the watch: Settings, About watch, Software, and tap "Build number" 7 times.
2. In Developer options turn on **ADB debugging** and **Debug over Wi-Fi**.
3. On the computer, with the watch on the same Wi-Fi network:

```
adb pair <ip>:<pairing port>
adb connect <ip>:<port>
adb install -r VPetWear-reloj.apk
```

4. On the watch open the app info for VPetWear and grant the permissions: notifications, physical activity and body sensors.

The watch app already includes its firmware and backgrounds: there is nothing to import for it to start.

## Automatic updates

Both apps look for new versions in this repository, in the `latest.json` file:

- **When:** when the app opens, at most once every 6 hours. Also by hand: on the phone, Settings, "App updates"; on the watch, Settings, "UPDATES".
- **What they do:** if there is a newer version they offer it once. When you accept, they download the APK, check it is the announced file (SHA-256) and Android asks you to confirm the install.
- **First time:** Android asks to allow the app to install other apps ("Install unknown apps"). You grant it once.
- **It only works between versions signed with the same key**, which are the ones in this repository.

Whoever publishes a new version must upload the APKs to a release named `VPetFarm-telefono.apk` and `VPetWear-reloj.apk`, and update `latest.json` with the version number, the download address and the SHA-256 of each file.

## Getting started

1. Open **VPetFarm** and create your account with your e-mail. The app sends a code to confirm it; if you forget the password, another code recovers it.
2. Pick or get your first Digimon on the farm.
3. Send your Digimon to the watch from the farm. The watch downloads the card it needs from the server, with no Bluetooth transfer.
4. Walk. The steps counted by the watch (and by the app, even when closed) fuel everything else.

## How it works

### Steps and blue points
- Every **1000 steps** give **10 blue points** spread over the stats.
- Each stat caps at **200** blue points.
- There is no daily step limit, but there is a maximum human pace to prevent cheating.

### Stats and rank
- Every Digimon has six stats (HP, MP, attack, defence, speed and brains).
- The **rank D to S** is the share of blue points already earned out of the maximum possible. It shows in the app and on the watch.
- The watch shows the same stats as the app, and they are the ones that count in battles.

### Training on the watch
Each training session (crunch, punch, dash, squat) gives **10 random blue points** among the stats, up to 200 per stat. The watch tells the server even when there is no connection at that moment.

### Mood and personality
- **Mood** goes from 0 to 100: it rises 10 with every win and drops 10 with every loss.
  - High mood (over 70): more experience and more attack and speed in combat.
  - Low mood (20 or less): less experience and less attack and speed.
- **Personality** (fierce, steady, calm or tricky) comes with the Digimon and decides how often it uses its special attack and how much it guards.

### Encounters and fights on the watch
- Every step adds **0.1%** to the chance of meeting a wild Digimon. The chance builds up, and after 1000 steps without a meeting there is a sure one. After each meeting the count starts again.
- The fight is automatic, one on one: attacks cross the screen, the rival takes the hit or dodges it and the attack flies on behind it.
- Win or lose, the scan goes up **5%**.
- A rival is never of a higher stage than your team.

### Evolution
- A Digimon evolves when it meets the rules of its card (time, vitals, wins and so on) **and** the tamer level allows that stage.
- If it is met on the watch, it evolves right there and the watch tells the server.

### Card adventure
On the farm, a Digimon walks the missions of its card in order, then fights the boss with the numbers the card gives it. Winning pays coins and experience and opens the next mission. On the watch you pick a zone of the card, see the step goal and the boss, and walk until you get there. The missions done are shared between the bracelet, the watch and the farm, and they open the evolutions that ask for the adventure.

### Online battles (phone)
From VPetFarm you face your team against other trainers. Battles are resolved on the server.

## Error reports

If an app crashes, it saves the error and sends it to the VPet server the next time it starts, so the problem can be fixed. A report has only the app version, the model of the phone or watch, the Android version and the text of the error: nothing about your account. Tokens, passwords and e-mail addresses are removed. On the phone you can turn it off in Settings, "Send error reports".

## Common problems

- **The watch does not connect with adb:** turn Wi-Fi debugging off and on again; the port changes every time.
- **It will not let me install:** uninstall the previous version; Android does not allow replacing an app signed with another key.
- **Steps do not go up when the app is closed:** on the phone remove the battery restriction for VPetFarm.
- **The watch says "Send one from your phone's farm":** there is no Digimon on the watch yet; send one from the farm.

## Credits and licenses

VPetWear and VPetFarm are modified versions of **VitalWear** (Christopher O'Grady, cfogrady) and **VBHelper** (nacabaro), both under the MIT license. Thanks to everyone who researched the Vital Bracelet and made those foundations possible.

Vital Bracelet, DIM, BEM and Digimon are trademarks of Bandai. This is a fan project, not affiliated with or endorsed by Bandai, and it is not distributed in app stores. The firmware, sprites and backgrounds that come with the installers are Bandai content and are included under the maintainer's responsibility. More details in [CREDITS.md](CREDITS.md), [LICENSE-VitalWear.txt](LICENSE-VitalWear.txt) and [LICENSE-VBHelper.txt](LICENSE-VBHelper.txt).
