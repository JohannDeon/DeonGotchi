# 🐾 DEONGotchi — The Haptic Companion

![Hardware Status](https://img.shields.io/badge/Hardware-ESP32--S3-orange)
![Interface](https://img.shields.io/badge/Interface-ST7789--LCD-blue)
![Audio](https://img.shields.io/badge/Audio-I2S--Haptic-brightgreen)

**DEONGotchi** est une console de poche "Virtual Pet" nouvelle génération. Conçue par **DEON**, elle repousse les limites du genre en intégrant des retours haptiques haute définition synchronisés sur le son et un moteur de rendu fluide sur ESP32-S3.

---

## ✨ Points Forts
- **🔊 Immersion Totale :** Grâce au mode *Audio-to-Vibe*, le DEONGotchi vibre physiquement au rythme de ses cris et de ses battements de cœur.
- **🚀 Performance S3 :** Utilisation de la PSRAM (8MB) pour des animations fluides sans ralentissement.
- **🎮 Contrôle Rétro :** Navigation via un joystick tactile 5 directions pour une sensation "D-Pad" authentique.
- **🔋 Autonomie Maximisée :** Régulateur LDO ultra-basse chute pour jouer jusqu'à la dernière goutte de la batterie LiPo.

---

## 🛠️ Architecture Matérielle



### Composants Clés
| Rôle | Référence | Protocole |
| :--- | :--- | :--- |
| **Cerveau** | ESP32-S3-WROOM-1-N16R8 | - |
| **Écran** | LCD TFT (Driver ST7789V) | SPI |
| **Audio** | MAX98357A (Amplificateur I2S) | I2S |
| **Haptique** | DRV2605L (LRA Driver) | I2C / Analog In |
| **Stockage** | Carte Micro SD | SDMMC (4-bit) |
| **Régulateur** | XC6220B331MR (900mA) | LDO |

### Configuration des Broches (Pinout)
Le DEONGotchi utilise une configuration optimisée pour éviter les conflits de mémoire (PSRAM) et les broches de strapping :

- **Navigation (Joystick) :** - UP: `GPIO 21` | DOWN: `GPIO 2` | LEFT: `GPIO 48` | RIGHT: `GPIO 47` | MID: `GPIO 1`
- **Audio I2S :** `GPIO 15` (LRCLK), `16` (BCLK), `17` (DIN)
- **Bus I2C :** `GPIO 4` (SDA), `5` (SCL)
- **SD Card :** Bus SDMMC 4-bit (D3 sur `GPIO 3`)

---

## 💻 Logiciel
Le firmware est conçu pour être modulaire. Il gère :
1. **Moteur Haptique :** Synchronisation temps réel entre la sortie audio I2S et l'entrée trigger du DRV2605L.
2. **Gestion SDMMC :** Chargement rapide des ressources graphiques depuis la carte SD.
3. **Menu System :** Interface utilisateur pilotée par interruptions pour une réactivité instantanée du D-Pad.



---

## 📦 Installation & Build
1. Clonez ce repository.
2. Ouvrez le projet sous **VS Code + PlatformIO**.
3. Sélectionnez l'environnement `esp32-s3-devkitc-1`.
4. Build & Upload.

---

## 📸 Galerie
*(Ajoutez ici vos photos du prototype et des captures d'écran du menu !)*

---

## 📜 Licence
Projet créé par **DEON**. Tous droits réservés.
