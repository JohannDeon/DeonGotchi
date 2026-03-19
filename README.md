
---

# 🐾 DEONGotchi — Console Open Source & Companion Polyvalent

![Brand](https://img.shields.io/badge/Brand-DEON%20electronics-blue)
![Hardware](https://img.shields.io/badge/Hardware-ESP32--S3--N16R8-orange)
![License](https://img.shields.io/badge/License-Open%20Source-green)

**DEONGotchi** est une console de poche **open source** basée sur **ESP32-S3**, pensée comme un **outil polyvalent** :

- 🎮 **Émulation de vieux jeux** (consoles rétro, mini-jeux maison)  
- 🧬 **Création d’environnements virtuels** ou “petits OS” faits maison  
- 🏠 **Contrôle de domotique** et d’objets connectés via **Wi-Fi** et **Bluetooth**  
- 🎨 Expérimentations en UI/UX, haptique, audio embarqué, etc.

Le but n’est pas seulement de faire un “Tamagotchi moderne”, mais une **plateforme modulaire** pour hacker, apprendre et prototyper des interfaces physiques interactives.

---

## 🎯 Objectifs du Projet

- **Open hardware & open firmware** : schémas, PCB, code et exemples publics.
- **Polyvalence** : pouvoir transformer le DEONGotchi en :
  - Mini-console d’émulation (NES-like, GB-like, jeux simples…)
  - Assistant virtuel, compagnon interactif, “petit OS” custom
  - Télécommande domotique (MQTT, HTTP, BLE, etc.)
  - Tableau de bord portable (capteurs, logs, notifications…)
- **Accessibilité développeur** : firmware en C/C++ (ESP-IDF / Arduino / PlatformIO) ou MicroPython selon préférence, avec exemples de projets.
- **Support des retours de la communauté** : contributions hardware / software encouragées.

---

## 🛠️ Matériel (BOM principale)

| Catégorie      | Référence                | Fonction                                        |
| -------------- | ------------------------ | ----------------------------------------------- |
| **MCU**        | ESP32-S3-WROOM-1-N16R8  | Dual-Core, Wi-Fi, BT, 16MB Flash, 8MB PSRAM     |
| **Alimentation** | XC6220B331MR           | LDO 3.3V 900mA, ultra low-dropout               |
| **Haptique**   | DRV2605LDGSR            | Pilote LRA haptique via I2C                     |
| **Audio**      | MAX98357AETE+T          | Ampli audio numérique I2S, Classe D             |
| **Affichage**  | HS20BS097RX             | Écran LCD / TFT haute clarté (SPI)              |
| **Joystick**   | TS-1095PS-A1B2-C3D2     | Switch multidirectionnel 5 positions            |
| **Stockage**   | µSD (SDMMC)             | Ressources, ROMs, assets, configs               |
| **Alim batterie** | LiPo + charge externe | Alimentation nomade                             |

---

## ⚙️ Configuration Hardware

### Gestion de l’énergie

Le **XC6220B331MR** assure un 3.3V stable même quand la LiPo chute sous ~3.4V, pour éviter les resets lors de pics de consommation (Wi‑Fi, audio, etc.).  
L’objectif est de garder le DEONGotchi **fiable** pour les usages longs (domotique, dashboard, jeux).

### Joystick 5 directions (Active-Low)

Le joystick est câblé en **logique active-bas**, avec GND commun :

- **UP** : GPIO 21  
- **DOWN** : GPIO 2  
- **LEFT** : GPIO 48  
- **RIGHT** : GPIO 47  
- **MID (clic / validation)** : GPIO 1  

Chaque direction est tirée à l’état haut via résistance de pull-up et passe à 0 (GND) lorsqu’on appuie.

### Audio & Haptique

- **Audio**  
  - Ampli **MAX98357A** en **I2S**  
  - Sortie vers un petit haut-parleur embarqué  
  - Utilisable pour : sons de jeux, retours audio UI, notifications domotiques, etc.

- **Vibreur / Haptique**  
  - Pilote **DRV2605L** en **I2C**  
  - GPIO SDA : 4 / SCL : 5  
  - Permet de jouer des motifs de vibration complexes (feedback pour UI, alertes domotiques, interactions de jeux…).

---

## 🧠 Capacités logicielles

Grâce aux **8MB de PSRAM**, le DEONGotchi peut :

- Stocker des **framebuffers** pour affichage fluide (jeux, animations).
- Gérer des **buffers audio** plus importants.
- Charger des **assets** (sprites, tilesets, polices, etc.) en mémoire.

### Périphériques et bus supportés

1. **I2C**  
   - DRV2605L (haptique)  
   - Capteurs additionnels possibles (IMU, température, etc.)  
   - Scanner I2C simple intégré au firmware d’exemple.

2. **SPI**  
   - Communication haute vitesse avec l’écran LCD/TFT  
   - Option pour d’autres périphériques SPI (flash externe, capteurs…)

3. **SDMMC / µSD**  
   - Stockage de :  
     - ROMs / jeux  
     - Assets graphiques  
     - Fichiers de config (Wi-Fi, profils domotiques, etc.)  
   - Peut servir de base à un petit système de fichiers pour un environnement custom.

4. **Wi-Fi & Bluetooth (ESP32-S3)**  
   - Wi-Fi : HTTP, MQTT, WebSocket, REST API, intégration domotique (Home Assistant, etc.)  
   - BLE : communication avec smartphone, capteurs, télécommandes personnalisées.

---

## 🕹️ Exemples de cas d’usage

- **Mini-console d’émulation**  
  - Lancer des émulateurs simples (8-bit / 16-bit light)  
  - Lire des ROMs depuis la carte µSD  
  - Utiliser le joystick + haptique + audio pour une expérience complète.

- **Enviro / OS custom**  
  - Interface type “companion digital”  
  - Affichage d’un environnement virtuel, d’un personnage, de stats, etc.  
  - Sauvegarde des états sur µSD.

- **Contrôleur domotique**  
  - Interface graphique avec menus pour piloter éclairages, volets, capteurs…  
  - Communication via Wi-Fi (MQTT, HTTP) ou BLE  
  - Retour haptique + audio pour confirmations d’actions.

- **Dashboard portable**  
  - Lecture de capteurs locaux ou réseau  
  - Affichage de graphiques, logs, notifications  
  - Utilisation comme “remote” pour un PC, un serveur, un cluster, etc.

---

## 🧩 Stack logicielle & Frameworks

Le projet vise à rester **flexible** : tu peux choisir ton environnement :

- **ESP-IDF** (officiel Espressif) pour un contrôle fin et des projets plus complexes
- **Arduino / PlatformIO** pour un onboarding rapide
- **MicroPython** / **CircuitPython** pour du prototypage rapide (si support adapté au S3 + PSRAM)

Le dépôt fournit (ou fournira) :

- Un **firmware de base** (menu, drivers écran/joystick/audio/I2C/SDMMC)
- Des **exemples de projets** :
  - Demo d’émulateur / jeu simple
  - Demo domotique (ex : client MQTT)
  - Demo companion / UI

---

## 🚧 État du projet

- [ ] Hardware Vx validé / en cours d’itération  
- [ ] Drivers de base (écran, audio, haptique, joystick)  
- [ ] SDK / exemples pour développeurs  
- [ ] Documentation d’API et tutoriels

Les informations peuvent évoluer, certaines parties sont encore expérimentales. N’hésite pas à ouvrir des issues / PR si tu repères des incohérences ou si tu veux proposer des améliorations.

---

## 🤝 Contribution

Les contributions sont bienvenues :

- **Hardware** : suggestions de composants, variantes de carte, shields ou docks.  
- **Software** : drivers, exemples, mini-jeux, intégrations domotiques, outils PC.  
- **Docs** : tutoriels, guides d’initiation, traductions.

Tu peux :

1. Fork le repo  
2. Créer une branche (`feature/ma-fonctionnalite`)  
3. Proposer une PR avec une description claire

---

## 🛡️ Licence & Crédits

- Projet open source initié par **DEON electronics**  
- Hardware & firmware publiés sous licences ouvertes (à préciser : MIT, GPL, CERN OHL, etc.)

---
