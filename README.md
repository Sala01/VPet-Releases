# VPet: granja de Digimon para el teléfono y el reloj

Proyecto de fans, gratuito y sin fines de lucro. Dos apps y un servidor:

| Pieza | Qué es | Archivo |
|---|---|---|
| **VPetFarm** | App de Android para el teléfono: tu granja, tus Digimon, tu cuenta | `VPetFarm-telefono.apk` |
| **VPetWear** | App de Wear OS para el reloj: tu Digimon camina, entrena y pelea contigo | `VPetWear-reloj.apk` |
| **Servidor** | Guarda tu progreso y arbitra las batallas (ya está en línea, no instalas nada) | — |

El progreso vive en el servidor: si cambias de teléfono o de reloj, tus Digimon siguen en tu cuenta.

Los instaladores están en [Releases](../../releases/latest). **Solo hay que instalar a mano la primera vez**: después las dos apps se actualizan solas (ver más abajo).

## Instalación

### Teléfono (VPetFarm)
1. Descarga `VPetFarm-telefono.apk` desde [Releases](../../releases/latest) en el teléfono y ábrelo.
2. Android pedirá permiso para instalar apps de esa fuente: acéptalo.
3. Si tenías una versión anterior firmada con otra llave (VBHelper original o una versión de prueba), desinstálala primero.

### Reloj (VPetWear)
El reloj no usa tienda: se instala desde una computadora con `adb`.

1. En el reloj: Ajustes, Acerca del reloj, Software, y toca 7 veces "Número de compilación".
2. En Opciones de desarrollador activa **Depuración ADB** y **Depuración por Wi-Fi**.
3. En la computadora, con el reloj en la misma red Wi-Fi:

```
adb pair <ip>:<puerto de emparejamiento>
adb connect <ip>:<puerto>
adb install -r VPetWear-reloj.apk
```

4. En el reloj abre la información de la app VPetWear y concede los permisos: notificaciones, actividad física y sensores corporales.

La app del reloj ya trae su firmware y sus fondos: no hay que importar nada para que arranque.

## Actualizaciones automáticas

Las dos apps buscan versiones nuevas en este repositorio, en el archivo `latest.json`:

- **Cuándo:** al abrir la app, como máximo una vez cada 6 horas. También a mano: en el teléfono, Ajustes, "App updates"; en el reloj, Ajustes, "UPDATES".
- **Qué hacen:** si hay una versión más nueva te la ofrecen una vez; al aceptar, descargan el APK, comprueban que es el archivo anunciado (SHA-256) y Android te pide confirmar la instalación.
- **Primera vez:** Android pide permitir que la app instale otras apps ("Instalar apps desconocidas"). Se concede una sola vez.
- **Solo funciona entre versiones firmadas con la misma llave**, que son las de este repositorio.

Quien publique una versión nueva debe subir los APK a un release con los nombres `VPetFarm-telefono.apk` y `VPetWear-reloj.apk`, y actualizar `latest.json` con el número de versión, la dirección de descarga y el SHA-256 de cada archivo.

## Primeros pasos

1. Abre **VPetFarm** y crea tu cuenta con tu correo. La app envía un código para confirmarlo; si olvidas la contraseña, otro código la recupera.
2. Elige o consigue tu primer Digimon en la granja.
3. Envía tu Digimon al reloj desde la granja. El reloj descarga la Card que necesita desde el servidor, sin pasar por Bluetooth.
4. Camina. Los pasos que cuenta el reloj (y la app, aun cerrada) son el combustible de todo lo demás.

## Cómo funciona

### Pasos y puntos azules
- Cada **1000 pasos** dan **10 puntos azules** repartidos en las estadísticas.
- Cada estadística tiene un tope de **200** puntos azules.
- No hay límite diario de pasos, pero sí un ritmo máximo humano para evitar trampas.

### Estadísticas y rango
- Cada Digimon tiene seis estadísticas (entre ellas HP, MP, ataque, defensa y velocidad).
- El **rango D a S** se calcula con la parte de los puntos azules ya conseguidos sobre el máximo posible. Se ve en la app y en el reloj.
- El reloj muestra las mismas estadísticas que la app, y son las que cuentan en las batallas.

### Entrenamiento en el reloj
Cada sesión de entrenamiento (abdominales, golpes, carrera, sentadillas) da **10 puntos azules al azar** entre las estadísticas, con el máximo de 200 por estadística. El reloj avisa al servidor aunque en ese momento no haya conexión.

### Humor y personalidad
- El **humor** va de 0 a 100: sube 10 con cada victoria y baja 10 con cada derrota.
  - Humor alto (más de 70): más experiencia y más ataque y velocidad en combate.
  - Humor bajo (20 o menos): menos experiencia y menos ataque y velocidad.
- La **personalidad** (feroz, firme, calmada o astuta) viene con el Digimon y decide qué tan seguido usa su ataque especial y cuánto se cubre.

### Encuentros y peleas en el reloj
- Cada paso suma **0.1 %** a la probabilidad de encontrar un Digimon salvaje. Esa probabilidad se acumula, y a los 1000 pasos sin encuentro hay uno seguro. Tras cada encuentro la cuenta vuelve a cero.
- La pelea es automática, uno contra uno: los ataques cruzan la pantalla, el rival recibe el golpe o lo esquiva y el ataque sigue de largo detrás de él.
- Ganes o pierdas, el escáner sube **5 %**.
- Un rival nunca es de una etapa mayor que la de tu equipo.

### Evolución
- El Digimon evoluciona cuando cumple las reglas de su Card (tiempo, vitales, victorias y demás) **y** el nivel de tamer permite esa etapa.
- Si se cumple en el reloj, evoluciona allí mismo y el reloj avisa al servidor.

### Aventura
Desde el menú del reloj eliges una zona de la Card, ves la meta de pasos y el jefe, y caminas hasta llegar. Puedes detenerla en cualquier momento. Se desbloquea a partir de la etapa Rookie.

### Batallas en línea (teléfono)
Desde VPetFarm enfrentas a tu equipo contra otros entrenadores. Las batallas se resuelven en el servidor.

## Problemas frecuentes

- **El reloj no se conecta con adb:** vuelve a activar la depuración por Wi-Fi; el puerto cambia cada vez.
- **No me deja instalar:** desinstala la versión anterior; Android no permite reemplazar una app firmada con otra llave.
- **Los pasos no suben con la app cerrada:** en el teléfono quita la restricción de batería a VPetFarm.
- **El reloj dice "Send one from your phone's farm":** aún no hay Digimon en el reloj; envíalo desde la granja.

## Créditos y licencias

VPetWear y VPetFarm son versiones modificadas de **VitalWear** (Christopher O'Grady, cfogrady) y **VBHelper** (nacabaro), ambos con licencia MIT. Gracias a todas las personas que investigaron el Vital Bracelet y a las que hicieron posibles esas bases.

Vital Bracelet, DIM, BEM y Digimon son marcas de Bandai. Este es un proyecto de fans, sin relación con Bandai ni respaldado por ella, y no se distribuye en tiendas de apps. El firmware, los sprites y los fondos que traen los instaladores son contenido de Bandai y se incluyen bajo responsabilidad del mantenedor. Más detalles en [CREDITS.md](CREDITS.md), [LICENSE-VitalWear.txt](LICENSE-VitalWear.txt) y [LICENSE-VBHelper.txt](LICENSE-VBHelper.txt).

---

# English summary

**VPet** is a free fan project: **VPetFarm** (Android phone app) and **VPetWear** (Wear OS app), backed by an online server that keeps your progress and referees the fights.

- **Updates:** both apps check `latest.json` in this repository when they open (at most every 6 hours) and offer the new version; you only install by hand once.
- **Phone:** open `VPetFarm-telefono.apk` from Releases and allow installs from that source.
- **Watch:** enable developer options, then `adb pair`, `adb connect`, `adb install -r VPetWear-reloj.apk`, and grant its permissions.
- **Start:** create an account in VPetFarm (the e-mail is confirmed with a code), get a Digimon, send it to the watch and walk.
- **Rules:** 1000 steps give 10 blue points (cap 200 per stat); each training session gives 10 random blue points; each step adds 0.1 % to the wild encounter chance (a sure meeting at 1000 steps); wins raise mood by 10 and losses lower it by 10; the rank goes from D to S; evolution follows the card's rules and the tamer level.
