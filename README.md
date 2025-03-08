# Adoucisseur d'eau - Capteur de niveau de sel / Water Softener - Salt Level Sensor

Schémat de montage : 

![schema de montage](images/schema.png)

Pour plus de simplicité j'ai utilisé une carte de type "terminal adapter for ESP32 30pin" : 


![Terminal adapter](https://www.theengineerstore.in/cdn/shop/products/3-2-314x252.jpg)

Les branchements se font de la même manière ils sont juste déportés.

Histoire de ne pas laisser pandouiller la carte dans le vide et de la laissé à la merci de la poussière, j'ai imprimé un petit boîtier pour la protéger : 

![image](https://media.printables.com/media/prints/595758/images/4744980_2a1c73e2-59dd-4ed8-b625-e7adb6d20a8e_5d2ce00b-0c34-46c5-a2e2-be2e6aeda27a/thumbs/inside/1280x960/jpg/img_20230927_164549.webp)

https://www.printables.com/model/595758-esp32-terminal-adapter-box

Idem pour le HC-sr04 : 

![image](https://media.printables.com/media/prints/42552/images/423052_cc9efe81-82ce-43f4-9e3f-c54c1321e22a/thumbs/cover/320x240/jpg/img_20201002_154350.webp)


https://www.printables.com/model/42552-hc-sr04-minimal-case

Le code est fait pour qu'il soit le plus simple à comprendre et à configurer, vous n'avez que 2 valeurs à changer (sans compter sur la config habituelle, api, ota et ap ) pour l'adapter à votre modèle d'adoucisseur d'eau : 

![config](images/config.png)






