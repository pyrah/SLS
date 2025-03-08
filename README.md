# Adoucisseur d'eau - Capteur de niveau de sel / Water Softener - Salt Level Sensor

## 🔧 Schéma de montage / Wiring Diagram

### Français 🇫🇷
Schéma de montage :

![Schéma de montage](images/schema.png)

Pour plus de simplicité, j'ai utilisé une carte **"Terminal Adapter for ESP32 30pin"** :  

![Terminal adapter](https://www.theengineerstore.in/cdn/shop/products/3-2-314x252.jpg)

Les branchements restent les mêmes, mais sont simplement déportés.

Pour éviter de laisser la carte **exposée à la poussière**, j'ai imprimé un boîtier de protection :  

![Boîtier ESP32](https://media.printables.com/media/prints/595758/images/4744980_2a1c73e2-59dd-4ed8-b625-e7adb6d20a8e_5d2ce00b-0c34-46c5-a2e2-be2e6aeda27a/thumbs/inside/1280x960/jpg/img_20230927_164549.webp)  

👉 [Télécharger le boîtier pour ESP32](https://www.printables.com/model/595758-esp32-terminal-adapter-box)

J'ai également imprimé un boîtier pour le **HC-SR04** :  

![Boîtier HC-SR04](https://media.printables.com/media/prints/42552/images/423052_cc9efe81-82ce-43f4-9e3f-c54c1321e22a/thumbs/cover/320x240/jpg/img_20201002_154350.webp)  

👉 [Télécharger le boîtier pour HC-SR04](https://www.printables.com/model/42552-hc-sr04-minimal-case)

---

### English 🇬🇧
### Wiring Diagram

Wiring diagram:

![Wiring diagram](images/schema.png)

To simplify the setup, I used a **"Terminal Adapter for ESP32 30pin"**:  

![Terminal adapter](https://www.theengineerstore.in/cdn/shop/products/3-2-314x252.jpg)

Connections remain the same but are simply extended.

To avoid leaving the board **exposed to dust**, I printed a protective case:  

![ESP32 Case](https://media.printables.com/media/prints/595758/images/4744980_2a1c73e2-59dd-4ed8-b625-e7adb6d20a8e_5d2ce00b-0c34-46c5-a2e2-be2e6aeda27a/thumbs/inside/1280x960/jpg/img_20230927_164549.webp)  

👉 [Download the ESP32 case](https://www.printables.com/model/595758-esp32-terminal-adapter-box)

I also printed a case for the **HC-SR04**:  

![HC-SR04 Case](https://media.printables.com/media/prints/42552/images/423052_cc9efe81-82ce-43f4-9e3f-c54c1321e22a/thumbs/cover/320x240/jpg/img_20201002_154350.webp)  

👉 [Download the HC-SR04 case](https://www.printables.com/model/42552-hc-sr04-minimal-case)

---

## ⚙️ Configuration

### Français 🇫🇷
Le code est conçu pour être **facile à comprendre et à configurer**.  
Vous n'avez que **2 valeurs à modifier** (hors configuration standard `api`, `ota`, et `ap`) pour l'adapter à votre adoucisseur d'eau :  

![Configuration](images/config.png)

### English 🇬🇧
The code is designed to be **easy to understand and configure**.  
You only need to **change 2 values** (excluding standard settings like `api`, `ota`, and `ap`) to adapt it to your water softener:  

![Configuration](images/config.png)

---

## ⚠️ Débogage et Avertissements / Debugging and Warnings

### Français 🇫🇷
Si vous voyez ce message dans les logs :  

```bash
[22:47:30][W][component:237]: Component template.sensor took a long time for an operation (52 ms).
[22:47:30][W][component:238]: Components should block for at most 30 ms.
```
Cela signifie que ESPHome recommande que chaque composant ne bloque pas l’exécution principale plus de 30 ms.
Ici, le template sensor (Percentage) met 52 ms, dépassant cette limite recommandée.
C’est un avertissement, pas une erreur, donc tout fonctionne normalement.

### English 🇬🇧
If you see this message in the logs:

```bash
[22:47:30][W][component:237]: Component template.sensor took a long time for an operation (52 ms).
[22:47:30][W][component:238]: Components should block for at most 30 ms.
```

It means that ESPHome recommends each component not block execution for more than 30 ms.
Here, the template sensor (Percentage) takes 52 ms, which exceeds the recommended limit.
It’s a warning, not an error, so everything still works fine.

## 📝 Code Optimisé / Optimized Code
```yaml
- platform: template
  name: "Percentage"
  unit_of_measurement: '%'
  icon: mdi:percent
  lambda: |-
    float distance_cm = id(salt_level_distance).state;
    float full = id(full_cm);
    float empty = id(empty_cm);
    float range = empty - full;
    float filled = empty - distance_cm;
    float percentage = (filled / range) * 100.0;

    // Réduction des logs pour améliorer la performance
    ESP_LOGD("DEBUG", "📏 Distance = %.2f cm | 🎯 full_cm = %.2f | 🛑 empty_cm = %.2f", distance_cm, full, empty);
    ESP_LOGD("DEBUG", "✅ Pourcentage = %.2f%%", percentage);

    return percentage;
```