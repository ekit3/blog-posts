---
layout: default-template
title:  "Feature Flipping"
date:   2023-07-27 9:00:00 +0200
categories: Architecture
author: [yohann_gueguin, maxime_montagne, jean_dusenne]
excerpt_separator: <!--END_SUMMARY-->
---

#####  Introduction

Ici nous allons parler de Feature Flipping, (que vous pouvez aussi connaitre sous le nom de Feature Toggles, Feature Switches, Feature Flag et bien d’autres encore), qui a pour principe de donner la possibilité de contrôler l’accès à des fonctionnalités de vos applications. 

Cette technique devient pertinente lorsque que par exemple, nous voulons mettre en place des fonctionnalités destinées à un public cible (beta user, premium user …), que nous souhaitons avoir plus de contrôle sur l’ensemble des services proposés par une application (possibilité de désactiver telle ou telle fonctionnalité pour maintenance, évolution, correctifs). 

 
Cette méthodologie peut être implémentée dans différents langage et de manière différente, cela va être à vous de choisir ce qui correspond le mieux à votre besoin. 
Il existe déjà des librairies, des Frameworks, et même des solutions SaaS pour répondre à ce besoin. 

![image](intro.jpg) <br/>
<!--END_SUMMARY-->

##  Quel intérêt pour la technique ? 

### Cycle de vie de livraison d’application

Le Feature Flipping apporte beaucoup de souplesse dans le cycle de vie d’une application et ce à plusieurs niveaux. 

D’abord l’équipe de développement va pouvoir désactiver tout ou partie du code source d’une ou de plusieurs features. Une feature non finalisée ou qu’on ne souhaite pas activer ne bloquera pas le déploiement d’une release complète. Ce qui ajoute énormément de liberté à l’équipe de développement dans ses réalisations. 

Ces features pourront être activées dans un second temps et n’empêchent donc pas le bon fonctionnement du processus de déploiement continu d’une application.  

### Graceful degradation & Progressive enhancement ( fr: Dégradation gracieuse & Amélioration progressive)

Cela permet aussi, lorsqu’on identifie un problème sur une fonctionnalité, de pouvoir la désactiver sans avoir besoin de déployer une nouvelle release. L’activation et la désactivation d’une feature peut se faire distinctement du déploiement d’une release. Imaginons que votre parcours de vente soit complétement bloqué à cause d’une étape facultative, la désactiver rendra le service à vos utilisateurs 

On peut également faire du déploiement “progressif” de fonctionnalités. C’est à dire, n’autoriser l’accès qu’à une poignée d’utilisateurs de l’application. Ainsi, cela permet à l’équipe de s’assurer de la pertinence d’une fonctionnalité avant un déploiement complet à l’ensemble des utilisateurs, et aussi potentiellement détecter des anomalies niveau applicatif ou infrastructure, qui n'avaient pas été anticipées. 

## Quel intérêt pour le Métier ?

### Tests A/B 

Dans l’agilité, nous parlons souvent du principe de l’empirisme. Ce principe se résume grosso-modo à l’apprentissage par l’expérience. L’A/B testing en est un bel exemple. Il permet de proposer des parcours différents de façon aléatoire afin de récolter des datas sur l’utilisation de l’application, et donc, de comprendre comment les utilisateurs l’utilisent en réalité. 

La mise en place de campagnes de test “A/B testing” est simple à comprendre, il permet de donner l’accès à différents parcours utilisateurs sur une même fonctionnalité ou encore de modifier graphiquement l’application pour avoir différents retours selon son utilisation. Ainsi, grâce aux données récoltées lors des campagnes de test, nous allons pouvoir valider une ou plusieurs hypothèses sur l’utilisation d’une ou de plusieurs fonctionnalités.  

Nous avons donc appris par l’expérience des utilisateurs que l’application devra s’orienter vers la version définitive d’une fonctionnalité qui correspond mieux aux besoins utilisateurs. 

### Fonctionnalités temporaires & Payantes 
 
Le feature flipping permet également de pouvoir activer des fonctionnalités uniquement lors de périodes spécifiques. Comme par exemple, un jeu ou un affichage spécifique pour la période de Noël, qu’on pourra désactiver une fois les fêtes terminées. 
Des modules activés uniquement en période de soldes, ou même des campagnes réservées aux premiers utilisateurs qui accéderons a la fonctionnalité. 
On peut également rapidement mettre en place un système pour gérer des fonctionnalités payantes de la même manière que pour les features temporaire, juste en changeant les critères de sélection. 

## Comment implémenter

Il existe un [site web](https://featureflags.io/) qui rassemble énormément de ressources autour de ce sujet, des guides, mais aussi une liste de librairies/SDKs. En le parcourant, nous nous rendons compte qu’il existe beaucoup de façons différentes de l’implémenter. 

Il existe plusieurs frameworks disponibles, parfois pour plusieurs langages de développement, nous pouvons retrouver par exemple, FF4J pour Java, FFLIP pour nodeJS ou encore Toggle pour Golang. 

On peut également retrouver des solutions Saas qui vont vous permettre via un SDK, (et bien sûr moyennant finance 😊), d’implémenter du feature flipping dans votre code, c’est le cas par exemple de launchdarkly, qui a un sdk disponible pour quasiment tous les langages du marché. 

Le plus intéressant serait peut-être de créer une solution maison, mais cela demanderait pas mal d’effort, et pourrait devenir vite complexe à gérer pour les différents langages qu’on peut utiliser. Cependant ! Il existe une solution open source, que vous pouvez déployer, via du conteneur dans votre infrastructure, compatible avec les langages les plus communs, il s’agit de Unleash qui apprait comme étant une solution très attrayante ! Mettant à disposition facilement une plateforme de gestion des features, facile à déployer et à maintenir, vous laissant également la possibilité d’y implémenter des fonctionnalités propres à vos besoin, compatible avec la plupart des langages, que demander de mieux ! 

## Quelques tests pour se faire un avis 

Pour tester rapidement, nous avons décidé de fabriquer une application web, développée en React, qui ferait appel à deux APIs différentes, une développée en NestJS, l’autre en Java Spring, pour justement activer ou non des features. 

Côté React nous avons utilisé [React Feature Toggles](https://github.com/paralleldrive/react-feature-toggles/), l'implémentation du feature flipping est assez simple coté front. Nous récupérons la liste des features et en fonction de leur disponibilité : les composants relatifs à ces features sont activés/chargés. 

Pour l’API Nestjs, nous avons utilisé [FFLIP](https://github.com/FredKSchott/fflip), plutôt simple à mettre en place, qui fonctionne avec un principe de critères qui peuvent être définis, calculés et cumulés, qui donnent accès à une ou plusieurs features. La simplicité d’utilisation et de compréhension permet une mutualisation rapide du code et le tout sans coût supplémentaire, contrairement à d’autres solutions Saas. 

Exemple d’un critère  

```javascript
{ 
    id: 'isPaidUser', 
    check: function (user, isPaid) { 
        return user.isPaid == isPaid; 
    }, 
} 
```

Exemple d’une feature  

```javascript
{ 
    id: 'newFeatureRollout', 
    // Si la feature est associée à une liste de critère, tous les critères doivent être évalués à vrai pour rendre accessible la feature à l’utilisateur 
    criteria: [ 
        { isPaidUser: true }, 
        { percentageOfUsers: 0.5 }, 
        { allowUserIDs: AllowEdIds }, 
    ], 
    enabled: true, 
} 
```

Exemple utilisation simple  

```javascript
let fflip = require('fflip'); 

 let Users = [ 
    { 
    id: 1, 
    name: 'Bob', 
    isPaid: false, 
    role: 'scrum', 
    canDrinkBeer: false, 
    } 
]; 

fflip.config({ 
    criteria: Criteria, // Une liste de critères comme définie plus haut 
    features: Features, // Une liste de feature comme définie plus haut 
}); 

console.log(fflip.getFeaturesForUser(Users[0])); 

let str: string;
const listName: string[] = Users.filter(user => fflip.isFeatureEnabledForUser('canDrinkBeer', user))
  .map(user => {
    console.log('Welcome to the Closed Beta!');
    str += `${user.name} can go drink some beer!\n`;
    return user.name;
  });
```

Pour finir, avec l’API Spring, nous avons essayé de mettre en place un système maison, afin de vérifier la possibilité de se passer de librairie ou solution tierce. Et le résultat est plutôt concluant, nous avons des résultats similaires entre les 2 APIs.  

Très grossièrement, pour imager à quoi ressemble un bout de code qui utilise du Feature Flipping, nous pourrions le résumer à un ensemble de “if”. 
 
Type implémentation simple 

``` 
    if Feature.is_enabled(‘new_feature’) 
        # new feature 
    else 
        # other 
    End 
```

Le Feature Flipping consiste à activer ou désactiver une fonctionnalité en fonction d’une variable, dynamiquement dans le code. 

 
Mais vous vous rendrez compte que c’est un peu plus complexe que cela, si vous le souhaitez, vous pouvez retrouver nos essais [ici](https://github.com/ekit3/feature-flipping). 

Au final il nous restait un bon nombre de librairies sur différentes technologies à tester, la liste étant longue, peu importe les affinités que vous avez dans les langages de développement vous trouverez de quoi essayer et pourquoi pas le mettre en place 

## Limites

### Multiplications des cas de tests 

Ce type de développement implique une grande rigueur quant au suivi et à la mise en place des tests autour de l’application. La multiplication des scénarios de tests et des différents parcours utilisateurs peut être une source de complication si le Feature Flipping n’est pas suivi ni appliqué correctement. Une grande rigueur est nécessaire de la part de toute l’équipe de développement.  

### Changement modèle de données 

Il ne faut pas oublier non plus que certaines modifications de fonctionnalités peuvent impliquer des impacts sur le modèle de données de l’application, ce qui peut rendre compliqué la cohabitation de plusieurs features. 
 
Le métier ne demandera pas le feature flipping pour les mêmes raisons (activation des features en fonctions des périodes, des profils utilisateurs) que le développement (faciliter le développement, le déploiement et rendre dispo la feature une fois terminée et testée)  

Alors, dans quelle mesure et jusqu’où peut-on aller avec le Feature Flipping ? 

### Quelques conseils 

Si vous deviez mettre en place le Feature Flipping, un premier conseil serait de le faire dès le début de vos projets ou de l’intégrer sur des nouvelles fonctionnalités indépendantes, cela peut représenter un gros travail de reprendre un système déjà en place.  

Il vous faudra également beaucoup de liant entre les équipes de développement, la qualité et le métier afin garantir une application parfaitement fonctionnelle de bout en bout. 
Mais ces efforts en valent la peine, vous n’aurez plus à attendre les tests de telle ou telle feature pour déployer, vous pourrez interagir plus facilement avec vos utilisateurs et mieux réagir en cas de problèmes. 