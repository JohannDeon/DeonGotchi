# 🐾 DEONGotchi — Haptic Companion Device

![Brand](https://img.shields.io/badge/Brand-DEON%20electronics-blue)
![Hardware](https://img.shields.io/badge/Hardware-ESP32--S3--N16R8-orange)


**DEONGotchi** est une console de poche haute performance dédiée à la simulation de vie artificielle. Développée par **DEON electronics**, elle combine une puissance de calcul élevée et une gestion fine de l'énergie pour une expérience utilisateur premium.

---

## 🛠️ Spécifications de la BOM (DEON electronics)

Le circuit a été optimisé avec des composants de précision pour garantir stabilité et réactivité.

### Composants Majeurs
| Catégorie | Référence | Fonction |
| :--- | :--- | :--- |
| **MCU** | ESP32-S3-WROOM-1-N16R8 | Processeur Dual-Core, 16MB Flash, 8MB PSRAM |
| **Alimentation** | XC6220B331MR | Régulateur LDO 900mA à ultra-faible chute de tension |
| **Haptique** | DRV2605LDGSR | Pilote de moteur vibrant (LRA) via I2C |
| **Audio** | MAX98357AETE+T | Amplificateur I2S Classe D (Audio numérique) |
| **Interface** | HS20BS097RX | Écran LCD haute clarté |
| **Joystick** | TS-1095PS-A1B2-C3D2 | Switch multidirectionnel 5 positions |



---

## 🏗️ Configuration du Hardware

### Gestion de l'Énergie
L'utilisation du **XC6220B331MR** permet au DEONGotchi de fonctionner de manière stable même lorsque la batterie LiPo descend sous les 3.4V, évitant les redémarrages intempestifs lors des pics de consommation du Wi-Fi ou du haut-parleur.

### Interface de Contrôle (5-Way Switch)
Le joystick est configuré en logique **Active-Low** (GND commun) :
- **UP** : GPIO 21
- **DOWN** : GPIO 2
- **LEFT** : GPIO 48
- **RIGHT** : GPIO 47
- **MID (Validation)** : GPIO 1

### Audio & Haptique
- **Audio :** Le MAX98357A décode le flux I2S pour le haut-parleur KLJ.
- **Vibreur :** Le DRV2605L est piloté exclusivement en **I2C** (SDA: GPIO 4 / SCL: GPIO 5), permettant de jouer des séquences de vibrations complexes indépendantes du son.

---

## 🚀 Développement Software
Le firmware exploite pleinement la **PSRAM de 8MB** pour stocker les buffers graphiques et les sons du compagnon, assurant une interface sans aucune latence.

1. **Protocole I2C :** Scanner pour détecter le DRV2605L et le capteur de mouvement.
2. **Protocole SPI :** Communication haute vitesse pour l'écran LCD.
3. **Système de fichiers :** Gestion des ressources sur Micro SD via SDMMC.

---

## 🛡️ Licence & Crédits
Propriété intellectuelle de **DEON electronics**. 
Conçu pour être le compagnon virtuel le plus technologique du marché.
