---
layout: default-template
title:  "PWA : Innovation ou solution de consolation ?"
date:   2021-09-29 9:00:00 +0200
categories: Front-End
author: [romain_vermeeren, yohann_gueguin, laurent_duchaussoy]
excerpt_separator: <!--END_SUMMARY-->
---

![image](pwa-dbz-img.jpg)

Le terme PWA est entré depuis quelques années dans le long répertoire des acronymes liés au numérique.
Mais qu’est ce qu’une `Progressive Web App` ?

Pour certains c’est la promesse d’une expérience mobile responsive boostée par les fonctionnalités de votre téléphone. Elle serait facile à mettre en place, de faible coût et elle n’aurait plus rien à envier aux applications natives.

Afin de vous éclairer sur le sujet et de vous permettre de vous faire votre propre avis, vous trouverez ici les informations qui nous paraissent pertinentes pour une première approche fonctionnelle du sujet.

<!--END_SUMMARY-->

![image](pwa-logo.png)

##### Mais d’où ça vient ?

La PWA est une suite logique de l’évolution du web sur mobile. Avant 2007 et l’arrivée des smartphones, l’accès mobile au web se fait par le WAP (Wireless Application Protocol). Il permet le téléchargement d’applications hors ligne non, dépendantes d’un réseau instable et peu performant. 

Après 2007 et avec la popularisation des smartphones arrive l’essor du développement mobile. Dès lors des solutions WEB tournent sur des technologies dynamiques exécutées côté serveur.
Steve Jobs imagine déjà des applications proches du principe de la PWA mais les principaux acteurs du marché font alors le choix de partir sur le développement d’applications natives permettant une meilleure UX et une meilleure intégration avec nos téléphones.

C’est en 2010 que l’arrivée de HTML5 et CSS3 va relancer les travaux autour d’applications hybrides et la mise en place de design responsive. 
On cherche alors à mutualiser le développement desktop et mobile.

Le terme PWA arrive en 2015 grâce à Alex Russell, l’un des ingénieurs ayant conceptualisé la solution chez Google. PWA: “Progressive Web Apps: Escaping Tabs Without Losing Our Soul”

Aujourd’hui les PWA sont supportées par une majorité de grandes entreprises de la tech (Google, Microsoft, Samsung, Mozilla, etc.) et utilisées par de nombreuses marques grand public (Starbucks, Pinterest, Spotify, etc.).

##### Oui mais ça consiste en quoi ?

Les Progressive Web Apps sont des versions optimisées d’un site web pour le mobile. Elles intégrent des fonctionnalités du téléphone, qui, jusqu’à aujourd’hui étaient réservées aux applications natives : appareil photo, mode hors ligne, raccourci écran d’accueil etc.
Elles sont considérées comme des `solutions Hybrides`. 
Supportées par le navigateur du téléphone, elles ne nécessitent pas de développement spécifique à l’OS et permettent la mutualisation des coûts de développement mobile et desktop.


#### 1- Un service Worker au coeur de l’application

Composant fondamental de la PWA, le service Worker est un script exécuté en tâche de fond qui va apporter toute l’intelligence à la PWA. Il intercepte les requêtes réseaux et y applique des configurations.
Il permet :

- Mise en cache du contenu
- Synchronisation des données en arrière plan
- Push de notifications
- L’utilisation des fonctionnalités de votre téléphone
- L’exécution d’actions hors ligne (comme pousser une bannière lorsque le téléphone est hors ligne)
- ...

#### 2- Un Manifest pour une expérience mobile

Le manifest, en plus du service worker, va permettre de transformer un site en PWA et de simuler une expérience native.
Il s’agit d’un simple fichier JSON dans lequel est configuré l’application et qui permet de la personnaliser.
Les utilisateurs pourront également installer directement un site web sur leur mobile ou leur desktop sans passer par les stores d’applications.

```json
{
    "name": "Blog Ekite",
    "short_name": "Blog Ekite",
    "description": "Blog Ekite.",
    "icons": [
        {
            "src": "assets/images/icons/icon-48.png",
            "sizes": "48x48",
            "type": "image/png"
        },
        {
            "src": "assets/images/icons/icon-72.png",
            "sizes": "72x72",
            "type": "image/png"
        },
        {
            "src": "assets/images/icons/icon-96.png",
            "sizes": "96x96",
            "type": "image/png"
        },
        {
            "src": "assets/images/icons/icon-128.png",
            "sizes": "128x128",
            "type": "image/png"
        },
        {
            "src": "assets/images/icons/icon-192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "assets/images/icons/icon-384.png",
            "sizes": "384x384",
            "type": "image/png"
        },
        {
            "src": "assets/images/icons/icon-512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ],
    "start_url": "/jekyll-site/",
    "display": "fullscreen",
    "theme_color": "#000000",
    "background_color": "#000000"
}
```

Configuration du raccourci de l'application mobile
- Nom
- URL
- Icone
- etc.

#### 3- Des APIs HTML5 pour les fonctionnalités

Le développement de PWA est grandement facilité par HTML5 qui propose la mise à disposition de nombreuses API aux navigateurs.
Ces API permettent, entre autres choses, l’utilisation de fonctionnalités telles que la géolocalisation, le push, le statut de la batterie, le presse papier, l’orientation de l’écran, les vibrations du mobile etc.
La liste détaillée de ces fonctionnalités est disponible sur ce [site](https://whatwebcando.today/){:target="_blank"}. 

![image](pwa-lighthouse.png)

Lighthouse est un plugin Chrome qui permet d’auditer un site web et qui indique son niveau de compatibilité avec la PWA.
Ce plugin liste l’ensemble des caractéristiques officielles qui permettent d’évaluer la performance des applications. 

<b>Progressive</b>
> Les applications web progressives fonctionnent sur n’importe quel périphérique et intègrent les fonctionnalités disponibles du navigateur et de l’appareil utilisé.

<b>Sécurisée</b>
> La mise en place d’un protocole HTTPS permet aux PWA d’être fiables et sûres, ce qui répond aux problématiques de sécurité des échanges entre les utilisateurs et les sites

<b>Engageante</b>
> Elles proposent une expérience utilisateur immersive en plein écran et facilitent le réengagement grâce à l’envoi de notifications push web.

<b>Installable</b>
> L’utilisation d’un fichier Manifest permet aux PWA de proposer, à l’instar d’une application mobile native, l’installation de l’application sur l’écran d’accueil du mobile.

<b>Rapidité</b>
> D’après Google, 53 % des internautes abandonnent un site si son chargement prend plus de trois secondes. Une fois le site chargé, la navigation doit se faire de manière rapide et fluide.

<b>Optimisation pour le référencement</b>
> Utilisant les technologies du web, les progressive web app peuvent être référencées sur les moteurs de recherche de la même manière que n’importe quel site web classique.

<b>Indépendante de la connexion</b>
> Grâce à la gestion du cache via l’utilisation d’un Service Worker, une fois le contenu chargé, il sera possible de le consulter même dans les zones de faible connexion réseau.

Sur le sujet de la mise en place et de la compatibilité avec les langages du marché, rien de particulier, la liste des frameworks est disponible ici :  [HNPWA](https://www.hnpwa.com/){:target="_blank"}

##### Donc pas mal d’avantages !

Les solutions PWA sont assez simples à mettre en place.
Elles ont une marge d’évolution relativement importante selon le temps et l’argent qui y sont consacrés.
D’un point de vue utilisateur, l’installation se fait de façon intuitive, sans même devoir passer par les stores. L’expérience utilisateur peut devenir aussi immersive que sur une application native. 

Les principaux avantages de la PWA sont, sans aucun doute, la fluidité, la fiabilité et la capacité à proposer des parcours hors ligne (grâce au chargement progressif) ainsi que l’optimisation de l’affichage sur mobile.
La co-construction avec le site web facilite l’organisation des équipes et permet la mutualisation des coûts de développement.

Sur un marché qui ne pense plus seulement à l’expérience utilisateur mais aussi à l’impact environnemental, ces différents avantages s’ancrent parfaitement dans des projets d’éco-conception : moins de données à héberger, un design optimisé pour une utilisation réduite de la batterie du mobile et surtout des phases de développement réduites contrairement à des projets d’application native.

##### Mais aussi des limites.

Vous avez peut-être entendu qu’Apple et PWA ne faisaient pas bon ménage. Malheureusement comme vous pourrez le constater dans ce [tableau des compatibilités](https://www.goodbarber.com/widget/browsers/){:target="_blank"}, les fonctionnalités disponibles sur Iphone et Safari sont, aujourd’hui encore, très limitées.
Il s’agit là du principal frein à la substitution des applications natives pour les entreprises fortement implantées sur mobile.

Il est également à noter que la mise en place d’une PWA nécessite une sécurisation de l’ensemble des pages de votre site par le protocole https. 

##### Qui fait de la PWA ?

Voici 2 exemples de PWA réussies:

<b>Twitter avec twitter lite: </b>

Objectifs: 
- Améliorer l’expérience sur les connexions limitées.
- Simplifier l’accès sans téléchargement sur les stores
- Optimiser par le cache et la taille des images
- Charger en amont pour une navigation hors ligne

Résultat:
- 65 % d’augmentation de pages vues par session
- 75 % d’augmentation de tweets envoyés
- 20 % de baisse du taux de rebond (comparé au site mobile avant PWA)

<b>ALIBABA (2016)</b>
Objectifs: 
- Augmenter le taux de conversion sur mobile
- Personnaliser l’ergonomie et le design sur la PWA
- Optimiser le chargement des images (nombreuses) pour se déployer sur les pays à faibles connections
- Fidéliser avec la proposition d’ajout du site sur l’écran d’accueil

Résultat:
- 76% de plus sur le taux de conversions sur tous les navigateurs (30% sur Android)
- 14% d’utilisateurs actifs mensuels en plus sur iOS
- 4X plus d’ajout à l’écran d’accueil

##### En conclusion

La PWA n’est ni une évolution des solutions mobiles natives ni une solution de consolation.<br>
Il s’agit d’une vraie réponse à des problématiques de déploiement sur mobile.<br/>
Elle offre une expérience immersive et intuitive pour l’utilisateur.
Sa mise en place est accessible à n’importe quelle taille de projet web.

Elle permet de rapidement mutualiser les coûts grâce à sa facilité de transformation.
Malheureusement son utilisation pour le développement de parcours innovants reste restreinte à cause de sa non-compatibilité avec les fonctionnalités natives des appareils IOS.

Aujourd’hui, la montée en puissance de cette technologie semble être conditionnée par Apple et leur volonté ou non d’améliorer la prise en charge des PWA. Après 5 ans d’existence, cette technologie n’a toujours pas réussi à percer.

Article de Laurent, Romain, Yohann, Septembre 2021

Glossaire:

<b>WAP:</b>C’est le premier protocole de communication qui a permis de relier le réseau mobile à internet

<b>Application Hybride:</b> contrairement aux applications natives qui utilisent directement les composants du device (mobile/tablette..), les applications hybrides utilisent le navigateur WEB embarqué dans le device et les technologies qu’on y retrouve pour le développement web, HTML, CSS, JavaScript

<b>Responsive:</b> le Responsive Web Design (RWD) est une technique qui consiste à ajuster automatiquement l’affichage d’une page web à la taille de l’écran du terminal utilisé

<b>Script:</b> suite de commandes qui permettent d’automatiser une tâche

<b>Stores d’application:</b> bibliothèque telle que l’Apple store ou le Play store qui permettent de trouver et d’installer des applications sur un téléphone

<b>Framework:</b> le regroupement d’outils qui facilitent le développement de logiciels et la création de systèmes (aussi appelé environnement de développement)

Sources:

- https://blog.octo.com/cest-quoi-une-progressive-web-app-pwa/
- https://fr.wikipedia.org/wiki/Progressive_web_app
- https://developer.mozilla.org/fr/docs/Web/Progressive_web_apps
- https://www.novaway.fr/blog/tech/3-exemples-pwa
- https://www.goodbarber.com/blog/progressive-web-apps-browser-support-compatibility-a883/
- https://developers.google.com/web/showcase/2017/twitter
- https://developers.google.com/web/showcase/2016/flipkart

