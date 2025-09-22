<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "26fd39046d264ba185dcb086d3a8cf3e",
  "translation_date": "2025-08-23T23:41:42+00:00",
  "source_file": "5-browser-extension/start/README.md",
  "language_code": "fr"
}
-->
# Extension de navigateur Carbon Trigger : Code de démarrage

En utilisant l'API CO2 Signal de tmrow pour suivre la consommation d'électricité, créez une extension de navigateur afin d'avoir un rappel directement dans votre navigateur sur l'intensité de la consommation d'électricité dans votre région. Utiliser cette extension de manière ponctuelle vous aidera à prendre des décisions sur vos activités en fonction de ces informations.

![capture d'écran de l'extension](../../../../5-browser-extension/extension-screenshot.png)

## Premiers pas

Vous devrez avoir [npm](https://npmjs.com) installé. Téléchargez une copie de ce code dans un dossier sur votre ordinateur.

Installez tous les packages nécessaires :

```
npm install
```

Construisez l'extension avec webpack :

```
npm run build
```

Pour l'installer sur Edge, utilisez le menu 'trois points' en haut à droite du navigateur pour accéder au panneau Extensions. À partir de là, sélectionnez 'Charger un pack non empaqueté' pour charger une nouvelle extension. Ouvrez le dossier 'dist' lorsque vous y êtes invité, et l'extension sera chargée. Pour l'utiliser, vous aurez besoin d'une clé API pour l'API CO2 Signal ([obtenez-en une ici par email](https://www.co2signal.com/) - entrez votre email dans la boîte sur cette page) et du [code de votre région](http://api.electricitymap.org/v3/zones) correspondant à la [Electricity Map](https://www.electricitymap.org/map) (à Boston, par exemple, j'utilise 'US-NEISO').

![installation](../../../../5-browser-extension/install-on-edge.png)

Une fois la clé API et la région saisies dans l'interface de l'extension, le point coloré dans la barre d'extension du navigateur devrait changer pour refléter la consommation énergétique de votre région et vous donner une indication sur les activités énergivores qui seraient appropriées à réaliser. Le concept derrière ce système de 'point' m'a été inspiré par l'extension [Energy Lollipop](https://energylollipop.com/) pour les émissions en Californie.

**Avertissement** :  
Ce document a été traduit à l'aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatisées peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant autorité. Pour des informations critiques, il est recommandé de recourir à une traduction humaine professionnelle. Nous déclinons toute responsabilité en cas de malentendus ou d'interprétations erronées résultant de l'utilisation de cette traduction.