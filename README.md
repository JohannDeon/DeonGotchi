# DeonGotchi

### **DeonGotchi : Le Tamagotchi Réinventé par Deon**

**NeoDeon** est un compagnon virtuel autonome alliant l'esthétique rétro des années 90 à une architecture matérielle de pointe. Conçu autour de l'**ESP32-S3**, ce projet dépasse le simple jouet électronique pour devenir une console haptique miniature capable de générer des interactions physiques synchronisées avec son environnement sonore.

#### **Cœur Technologique**

Le projet est piloté par le script central **`MapToMeshGenerator`**, qui gère la logique de vie de la créature et l'affichage fluide sur un écran LCD **ST7789V**. Grâce aux 8 Mo de PSRAM du module S3, l'appareil peut traiter des animations complexes stockées sur une carte SD via un bus **SDMMC 4-bits** ultra-rapide.

#### **Expérience Sensorielle Immersive**

NeoDeon se distingue par sa capacité à "ressentir" et à "émettre" :

* **Audio-Haptique :** L'amplificateur **MAX98357A** délivre un son clair au haut-parleur de 0.7W. Simultanément, le pilote **DRV2605L** analyse le flux audio pour faire vibrer le moteur LRA, permettant au compagnon de vibrer physiquement au rythme de ses propres cris.
* **Interactivité :** Un gyroscope/accéléromètre I2C détecte les mouvements du joueur, permettant de réveiller la créature en secouant l'appareil.

#### **Interface et Ergonomie**

Le contrôle est assuré par un switch tactile à 5 directions (D-pad numérique), offrant une navigation précise dans les menus sans encombrer l'écran.

#### **Gestion de l'Énergie**

Optimisé pour la mobilité, NeoDeon intègre un régulateur **XC6220B331MR** à très faible chute de tension. Ce choix garantit un fonctionnement stable à 3.3V jusqu'à l'épuisement de la batterie LiPo, tout en supportant les pics de courant du Wi-Fi et du moteur haptique.

---

**NeoDeon** n'est pas qu'un simulateur de vie ; c'est une démonstration de force technique où chaque GPIO de l'ESP32-S3 a été optimisé pour créer l'animal de compagnie virtuel le plus vivant jamais conçu par un maker.
