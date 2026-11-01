# VPet installers

Installable versions of **VPetWear** (Wear OS) and **VPetFarm** (Android phone). The source code is
private. This repository only has the installers, the licenses and the credits.

| App | What it is | File |
|---|---|---|
| **VPetWear** | Digital pet for Wear OS watches. Modified version of VitalWear. | `VPetWear-watch-v0.1.0.apk` |
| **VPetWear Companion** | Phone app that sends cards and characters to the watch. | `VPetWear-companion-v0.1.0.apk` |
| **VPetFarm** | Phone app to raise, evolve and send your partners. Modified version of VBHelper. | `VPetFarm-v0.1.0.apk` |

Download them from [Releases](../../releases).

## Install

**Phone (VPetFarm and VPetWear Companion):** download the APK and open it. Android asks you to allow
installing from that source.

**Watch (VPetWear):** it is not on a store, so it is installed with `adb`.
1. On the watch open Settings, About watch, Software, and tap Build number 7 times.
2. In Developer options turn on ADB debugging and Debug over Wi-Fi.
3. On the PC, with the watch on the same Wi-Fi:

```
adb pair <ip>:<pairing port>
adb connect <ip>:<port>
adb install VPetWear-watch-v0.1.0.apk
```

4. On the watch, open App info for VPetWear and allow its permissions (notifications, physical
   activity and body sensors).

The watch app already includes its firmware, sprites and a default background, so nothing has to
be imported for it to start.

## Use

1. Open **VPetWear Companion** on the phone, choose Import Card Image and pick a DIM or BEM `.bin`.
   The card is sent to the watch. It no longer has to be verified with a bracelet.
2. In **VPetFarm**, open a partner and choose Send to VPetWear. The watch receives it and makes it
   the active character.

A different background can be placed as `background.png`, `background.jpg` or `background.webp` in
`Android/data/com.github.cfogrady.vitalwear/files` on the watch.

## Good to know

- These builds are signed with the maintainer's own key. If you have the original VitalWear or
  VBHelper installed, uninstall it first, because Android doesn't let one app replace another
  signed with a different key. The same goes for earlier debug builds.
- Cards created by the community work too, as any `.bin` can be imported.

## Credits and licenses

VPetWear and VPetFarm are modified versions of **VitalWear** by Christopher O'Grady (cfogrady) and
**VBHelper** by nacabaro, both under the MIT license. See [CREDITS.md](CREDITS.md),
[LICENSE-VitalWear.txt](LICENSE-VitalWear.txt) and [LICENSE-VBHelper.txt](LICENSE-VBHelper.txt).
Thanks to everyone credited there for the code and research this is built on.

## Bandai

Vital Bracelet, DIM, BEM and Digimon are trademarks of Bandai, and this project is not affiliated
with or endorsed by Bandai. The firmware, sprites and background image in the installers are
Bandai content. They are included on the maintainer's responsibility, based on Bandai's notice
that the Vital Bracelet series is discontinued and its content may be used by the community. A link
to that notice will be added here.

---

# Instaladores de VPet (español)

Versiones instalables de **VPetWear** (Wear OS) y **VPetFarm** (teléfono Android). El código fuente
es privado. Este repositorio solo tiene los instaladores, las licencias y los créditos.

- **Teléfono:** descarga el APK y ábrelo.
- **Reloj:** se instala con `adb` (pasos arriba). La app del reloj ya incluye el firmware, los
  sprites y un fondo por defecto.
- **Uso:** importa una Card `.bin` con VPetWear Companion, y envía un Digimon desde VPetFarm con
  Send to VPetWear.
- **Importante:** si tienes instalados VitalWear o VBHelper originales, desinstálalos antes, porque
  están firmados con otra llave.
