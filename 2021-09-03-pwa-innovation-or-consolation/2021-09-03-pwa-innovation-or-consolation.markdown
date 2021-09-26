---
layout: default-template
title:  "PWA : Innovation ou solution de consolation ?"
date:   2021-09-03 18:00:00 -0600
categories: front-end
author: romain_vermeeren
excerpt_separator: <!--END_SUMMARY-->
---

![image](pwa-dbz-img.jpg)

Le terme PWA est entré depuis quelques années dans le long répertoire des acronymes liés au numérique.
Mais qu’est ce qu’une `Progressive Web App` ? Vu par certains comme la promesse d’une expérience mobile responsive boosté par les fonctionnalités de votre téléphone, elle serait facile à mettre en place, de faible coût et n'aurait plus rien à envier aux applications natives.
Afin de vous éclairer sur le sujet et vous permettre de vous faire votre propre avis, nous avons rassemblé ici les informations qui nous paraissent pertinentes pour une première approche fonctionnelle du sujet. 

<!--END_SUMMARY-->

![image](pwa-logo.png)

##### Mais d’où ça vient ?

La PWA est une suite logique de l’évolution du web sur mobile.
Avant 2007 et l’arrivée des smartphones, l’accès mobile au web se fait par le WAP.
Il permet le téléchargement d'applications hors ligne non dépendantes d’un réseau instable et peu performant. 

L’après 2007 et la popularisation des smartphones entraîne l’essor du développement mobile au moment où les solutions WEB tournent sur des technologies dynamiques exécutées côté serveur.
Steve Jobs imagine déjà des applications proche du principe de la PWA mais les principaux acteurs du marché font alors le choix de partir sur le développement d'applications natives permettant une meilleure UX et une meilleure intégration avec nos téléphones.

C’est en 2010 que l’arrivée de HTML5 et CSS3 va relancer les travaux autour d'applications hybrides et la mise en place de design responsive.
On cherche alors à mutualiser le développement desktop et mobile.

Le terme PWA arrive en 2015 de la bouche d’Alex Russell, l’un des ingénieurs ayant conceptualisé la solution chez Google.
PWA: “Progressive Web Apps: Escaping Tabs Without Losing Our Soul”

Aujourd’hui les PWA sont supportés par une majorité de grandes entreprises de la tech (Google, Microsoft, Samsung, Mozilla, etc.) et utilisées par de nombreuses marques grand public (Starbucks, Pinterest, Spotify, etc.).

##### Oui mais ça consiste en quoi ?

Les Progressive Web Apps sont des versions optimisées d’un site web pour le mobile mais intégrant des fonctionnalités du téléphone qui jusqu’à aujourd’hui étaient réservées aux applications natives: prise de photo, mode hors ligne, raccourcie sur l’écran d’accueil etc.
Elles sont considérés comme des `solutions Hybrides`.
Supportées par le navigateur du téléphone, elles ne nécessitent pas de développement spécifique à l’OS et permettent la mutualisation des coûts de développement mobile et desktop.


#### 1- Un service Worker au coeur de l’application

Composante fondamentale de la PWA, il s’agit d’un script exécuté en tâche de fond qui va apporter toute l'intelligence à la PWA en interceptant les requêtes réseaux et en y appliquant des configurations. 
Il permet :
- Mise en cache du contenu
- Synchronisation des données en arrière plan
- Push de notifications
- Utiliser les fonctionnalités de votre téléphone
- Il peut également effectuer des actions hors ligne comme pousser une bannière lorsque le téléphone est hors ligne
- etc.

#### 2- Un Manifest pour une expérience mobile

Le manifest, en plus du service worker, va vous permettre de transformer votre site en PWA et de simuler une expérience native.
Il s'agit d’un simple fichier JSON dans lequel vous allez configurer et personnaliser votre application.
Cela permet également aux utilisateurs d'installer directement votre site web sur leur mobile ou leur desktop sans passer par les stores d’application.

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

Le développement des PWA s’est vû grandement facilité par HTML5 qui proposent de nombreuses API mises à disposition des navigateurs.
Permettant, entre autres, l’utilisation de fonctionnalités de géolocalisation, push, status de la batterie, presse papier, orientation de l’écran, les vibrations du mobile etc.
Vous pouvez retrouver la liste de ces fonctionnalités détaillées sur ce [site](https://whatwebcando.today/){:target="_blank"}. 

![image](pwa-lighthouse.png)

Ci-après la liste des caractéristiques officielles que vous pouvez retrouver dans Lighthouse afin d’évaluer la performance de vos applications.
Lighthouse est un plugin Chrome permettant d’auditer votre site web qui vous donnera son niveau de compatibilité avec la PWA.

<b>Progressive</b>
> Les applications web progressives fonctionnent sur n'importe quel périphérique en intégrant les fonctionnalités disponibles du navigateur et de l'appareil utilisé.

<b>Sécurisée</b>
> Afin de répondre aux problématiques de sécurité des échanges entre les utilisateurs et les sites, les PWA doivent être fiables et sûres par la mise en place d’un protocole HTTPS.

<b>Engageante</b>
> Elles proposent une expérience utilisateur immersive en plein écran et un réengagement facilité grâce à l'envoi de notifications push web.

<b>Installable</b>
> L'utilisation d'un fichier Manifest permet aux PWA de proposer, à l'instar d'une application mobile native, l'installation de l’application sur l'écran d'accueil du terminal mobile.

<b>Rapidité</b>
> D'après Google, 53 % des internautes abandonnent un site si le chargement prend plus de trois secondes. Une fois le site chargé, la navigation doit se faire de manière rapide et fluide.

<b>Optimisation pour le référencement</b>
> Utilisant les technologies du web, les progressive web app peuvent être référencées sur les moteurs de recherche de la même manière que n'importe quel site web classique.

<b>Indépendante de la connexion</b>
> Grâce à la gestion du cache via l’utilisation d’un Service Worker, une fois le contenu chargé une première fois, il est possible de le consulter même dans les zones de faible connexion réseau.

D’un point de vue mise en place et compatibilité avec les langages du marché, rien d’exotique. 
Vous pouvez retrouver la liste des framework disponible ici:  [HNPWA](https://www.hnpwa.com/){:target="_blank"}

##### Donc pas mal d’avantages !

Les solution PWA sont donc assez simples à mettre en place et ont une marge d’évolution relativement importante selon le temps et l’argent qu’on y consacre.
D’un point de vue utilisateur, l’installation se fait de façon intuitive sans même avoir à passer par les stores.
L’expérience utilisateur peut devenir aussi immersive que sur une application native.
Les avantages principaux de la PWA sont sans aucun doute sa fluidité et sa fiabilité grâce au chargement progressif, sa capacité à proposer des parcours hors ligne ou encore par l’optimisation de l’affichage sur mobile.
La co-construction avec le site web facilite l’organisation des équipes et permet de mutualiser les coûts de développement. 

Sur un marché qui ne pense plus seulement à l’expérience utilisateur mais également à l'impact environnemental.
Ces différents avantages s'ancrent parfaitement dans des projets d’éco-conception.
Moins de données à héberger, un design optimisé pour une utilisation réduite de la batterie de votre mobile mais surtout des phases de développement réduite contrairement à un projet d’application native.

##### Mais aussi des limites.

Vous avez peut être entendu que Apple et PWA ne faisaient pas bon ménage, et malheuresement comme vous pouvez le constater dans le [tableau des compatibilités](https://www.goodbarber.com/widget/browsers/){:target="_blank"}, les fonctionnalités disponibles sur Iphone et Safari sont aujourd'hui encore très limitées.
Il s’agit là du principal frein à la substitution des applications natives pour les entreprises fortement implantées sur mobile. 

Il est également à noter que la mise en place d’une PWA nécessite une sécurisation de l’ensemble des pages de votre site par le protocole https. 

##### Qui fait de la PWA ?

Voici 2 exemples de PWA réussies:

<b>Twitter avec twitter lite: </b>

Objectifs: 
- améliorer l’expérience sur les connexions limitées.
- un accès simplifié sans téléchargement sur les stores
- optimisation par le cache et la taille des images
- Chargement en amont pour une navigation hors ligne

Résultat:
- 65 % d’augmentation de pages par session
- 75 % d’augmentation des tweets envoyés
- 20 % de baisse du taux de rebond comparé au site mobile avant PWA.

<b>ALIBABA (2016): </b>
Objectifs: augmenter le taux de conversion sur mobile
- Personnalisation de l’ergonomie et du design sur la PWA
- Optimisation du chargement des images (nombreuses) pour se déployer sur les pays à faibles connections
- Fidélisation avec la proposition d’ajouter le site à l’écran d'accueil

Résultat:
- 76% de conversions en plus sur tous les navigateurs 30% sur Android 
- 14% d'utilisateurs actifs mensuels en plus sur iOS
- 4X plus d’ajout à l'écran d'accueil 

##### En conclusion

La pwa n’est donc ni une évolution des solutions mobiles natives ni une solution de consolation.<br>
Il s’agit d’une vraie réponse aux problématiques de déploiement sur mobile.<br>
Elle offre une expérience immersive, intuitive pour l’utilisateur et sa mise en place est accessible à n'importe quelle taille de projet web.<br>
Elle permet de rapidement mutualiser les coûts grâce à sa facilité de transformation.<br>
Malheureusement son utilisation pour le développement de parcours innovants reste restreinte de par sa non compatibilité avec les fonctionnalités native des appareils IOS.<br>
Aujourd’hui la montée en puissance de cette technologie semble être conditionnée par Apple et sa volonté ou non d’améliorer sa prise en charge.
Après 5 ans d'existence, cette technologie n’a aujourd’hui pas encore réussi à percer. 

Glossaire:

<b>WAP:</b>C’est le premier protocole de communication qui a permis de relier le réseau mobile à internet.

<b>Application Hybride:</b> Une application hybride, contrairement aux applications natives qui utilisent directement les composants du device (mobile/tablette..), utilise le navigateur WEB embarqué dans le device & les technologies qu’on retrouve dans le développement web, HTML, CSS, JavaScript.

<b>Responsive:</b> Le Responsive Web Design (RWD) est une technique qui consiste à ajuster automatiquement l’affichage d’une page web à la taille d’écran du terminal utilisé.

<b>Script:</b> Suite de commandes permettant d'automatiser une tâche.

<b>Stores d’application:</b> Bibliothèque tel que l’Apple store ou le Play store permettant de trouver et d’installer des applications sur son téléphone.

<b>Framework:</b> Un Framework est le regroupement d’outils facilitant le développement de logiciels et la création de systèmes. Aussi appelé environnement de développement.

Sources:

- https://blog.octo.com/cest-quoi-une-progressive-web-app-pwa/
- https://fr.wikipedia.org/wiki/Progressive_web_app
- https://developer.mozilla.org/fr/docs/Web/Progressive_web_apps
- https://www.novaway.fr/blog/tech/3-exemples-pwa
- https://www.goodbarber.com/blog/progressive-web-apps-browser-support-compatibility-a883/
- https://developers.google.com/web/showcase/2017/twitter
- https://developers.google.com/web/showcase/2016/flipkart

