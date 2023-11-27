--- 
title: "\"Cas d'étude : Spring\"" 
description: '"Etude de cas DevOps sur Spring"' 
"date:": 2023-11-10 
authors: "[Maxime ALLEMEERSCH, Louis CAVRENNE, Alexandre HENROTTE]" 
tags: [spring, devops, vmware, vmware-tanzu, agile, ci-cd, automatisation, management]
---

# Introduction

Un des cours qui est donné à la Faculté Informatique de l’Université de Namur est le cours d’Automated Software Engineering. Dans le cadre de celui-ci, il nous est demandé de réaliser des recherches sur le fonctionnement de divers projets open source concernant leur organisation et leur méthodologie de développement (DevOps, agile, etc.).

Le projet que nous avons sélectionné est le framework Spring, développé par VMware. Nous nous sommes penchés sur celui-ci car sa présence importante sur le marché nous a laissé penser que nous pourrions très facilement trouver de la documentation ainsi que des informations sur ces éléments à chercher.

# Description du cas d'étude

## Contexte et domaine d'application

Les entreprises développant des produits logiciels ont de plus en plus recours à des frameworks (cadriciel en français) pour les aider pendant leur phase de développement. Ceux-ci offrent une base commune pour que les développeurs n’aient pas à repartir de zéro et de nombreux outils y sont inclus pour grandement faciliter la mise en place d’applications et services divers. De cette manière, ces "boites à outils" éliminent une grande partie du travail et font gagner beaucoup de temps et d'efficacité aux entreprises. Les frameworks visent à éviter aux développeurs de devoir réinventer la roue.

Spring est un framework open source sur lequel peut être développé n’importe quelle application Java, généralement des applications web ou des back-ends exposant une API REST. Spring est très largement utilisé dans le monde de l’entreprise. Les grands avantages de ce framework résident dans sa légèreté, sa rapidité et sa modularité.

## Description générale des fonctionnalités offertes

Pour simplifier les différentes complexités techniques auxquelles font souvent face les développeurs lorsque lorsqu’ils développent une application d’entreprise, le framework Spring offre de nombreuses fonctionnalités pour faciliter et renforcer le développement :

- **Technologies de base** : injection de dépendances, événements, ressources, i18n, validation, data binding, conversion de types, SpEL, AOP. 

- **Tests** : objets mock, TestContext framework, Spring MVC Test, WebTestClient. 

- **Accès aux données** : transactions, support DAO, JDBC, ORM, Marshalling XML. 

- Frameworks web Spring MVC et Spring WebFlux. 

- **Intégration** : remoting, JMS, JCA, JMX, courrier électronique, tâches, planification, cache et observabilité. 

- **Langages** : Kotlin, Groovy, langages dynamiques.

# Analyse DevOps du cas d'étude

## Identification des facteurs mis en place favorisant le DevOps  

### Lead time

La métrique de "lead time" permet de mesurer le temps que prend une fonctionnalité à être complètement implémentée, depuis son initialisation jusqu'à sa complétion. 

Pour favoriser cette mesure, plusieurs facteurs sont mis en place. 

Premièrement, l'incontournable gestionnaire de versions Git est utilisé pour gérer les différentes versions du projet et de permettre un développement des différentes fonctionnalités en parallèle. Cet outil propose ainsi un système de branches et de commits. Le plus célèbre est GitHub, utilisé ici par le projet. 

En deuxième lieu, on retrouve également en tendance chez les développeurs pour ce projet la création de petits commits au sein du dépôt de code, ceux-ci favorisant une clarté dans l’historique des modifications et une meilleure traçabilité pour remonter d’occasionnels bugs. Dans cette même logique, toutes les modifications et ajouts de fonctionnalités sont créés dans des branches bien distinctes les unes des autres. Les features sont ajoutées de façon indépendante, ce qui permet une meilleure séparation et distribution des tâches. Ces nouvelles fonctionnalités sont alors fusionnées avec des branches plus importantes par le biais de petites pull requests. On peut clairement identifier cette façon de fonctionner dans le dépôt du projet. 

Une autre façon de minimiser le temps pour la métrique du "lead time" est de maximiser le nombre de releases pour le projet. On effectue pour Spring en moyenne 2 à 3 releases par mois, ces releases incluant toutes les nouvelles fonctionnalités ainsi que toutes les corrections de bugs effectuées. Ces releases comprennent également des améliorations dans la documentation mais également des mises à jour de dépendances à d'autres outils et projets. 

Sont également utilisés dans le projet les GitHub Actions. Celles-ci consistent en des processus prédéfinis qui sont exécutés automatiquement à certains moments clés. Des builds automatisés sont ici utilisés dans le projet. 

Enfin, pour orchestrer l'ajout de code par les différents contributeurs extérieurs à VMware, il existe une série de guidelines. On retrouve un code de conduite ainsi qu’une définition sur l’ajout de code et comment efficacement rédiger celui-ci.

### Deployment frequency

Cette métrique s'intéresse au nombre de fois qu’une version d’un produit est mise en production. 

Ici, Spring Framework déploie une version principale du projet sur la branche principale une fois par an. Des versions mineures sont tout de même publiées, comme expliqué dans l'analyse de la première métrique DORA. 

Ces versions principales sont supportées et maintenues pendant une période de deux ans, ce qui laisse le temps aux développeurs utilisant le framework de migrer sur une version plus récente pour rester à jour sur les nouvelles fonctionnalités et mises à jour de sécurité. 

Des versions LTS (pour Long Time Supported) sont des versions qui restent plus longtemps maintenues. Spring déploie une version LTS tous les 4 ans.  À l'heure actuelle, la plus récente est la version `5.3`. 

Il est à noter que des versions tests, appelées versions "snapshot", sont également mises en production à une fréquence moins régulière et plus aléatoire. En ce qui concerne les correctifs, ils sont déployés une fois par mois.

### Mean time to restore 

Il s'agit de la mesure du temps qu'il faut compter pour qu'une erreur soit fixée et déployée en production. 

Le code source du projet étant hébergé sur GitHub, il est possible aux utilisateurs d’analyser en profondeur la manière dont les fonctionnalités sont implémentées et reporter les erreurs de développements qui peuvent provoquer des fautes et erreurs. Un de ces avantages de l’open source, combiné à un système de reporting d'erreurs, permet à un projet de très facilement pointer la source à un problème et planifier et mettre en œuvre des corrections. Spring permet également aux collaborateurs externes d'apporter leurs propres correctifs, ce qui réduit efficacement le temps d’attente pour un fix provenant de l’équipe chez VMware Tanzu. 

Les employés chez cette dernière sont très réactifs et acceptent rapidement ces correctifs au sein des branches pour les prochaines versions du projet. 

Avant d'accepter toutes formes de modification dans une branche de release, une série de tests automatiques est exécutée pour s'assurer de la stabilité du code produit. 

Enfin, sans réellement trouver de chiffres exacts, on peut supposer que cette métrique est très petite. Cette supposition se construit autour du fait que pour des erreurs critiques trouvées au sein d’une version en production, des correctifs d’urgence peuvent être produits et déployés par l'équipe de développement. Un exemple parmi d’autres est une faille de sécurité de type RCE (Remote Code Execution) qui a été découverte en 2022 par un utilisateur du framework. Un correctif d’urgence a été mis en production deux jours après que cet utilisateur l'ait reporté en interne à l’équipe chez VMware. VMWare Tanzu opte pour la transparence lors de ce genre d’événement en publiant régulièrement sur le [blog](https://spring.io/blog/) du framework.

### Change fail percentage 

Il est compliqué de deviner cette métrique qui s'intéresse au pourcentage de déploiements provoquant une erreur en production si les chiffres ne sont pas implicitement communiqués. La meilleure solution est d’étudier la fréquence des commits qui sont effectués et celle du nombre d’issues qui sont ouvertes et fermées. 

Ci-dessous sont listés les chiffres que l’on peut trouver à l’aide de l’outil d’analyse de projet sur le dépôt du projet sur GitHub. Ceux-ci datent du mois dernier.

**En un mois** 

- 458 issues clôturées 

- 39 issues ouvertes 

- 219 commits ajoutés dans la branche principale (en faisant utilisation d’une stratégie de "squash commit" lors de la fusion d’une branche dans une autre)

**Globalement**

- 23467 issues clôturées 

- 729 issues ouvertes

## Description du pipeline de développement

### Planification et Conception

Spring est un projet open source géré par la communauté. La planification est donc influencée par les retours des utilisateurs, les contributions de la communauté et les besoins de l'écosystème Java. 

Spring suit un cycle de versions régulier. Les versions majeures peuvent introduire des changements importants, tandis que les versions mineures apportent généralement des améliorations et des correctifs de bugs. 

L'évolution de Spring avec les standards Java constitue une approche fondamentale pour garantir la capacité des outils à communiquer entre eux et la compatibilité avec l'écosystème Java. Spring s'efforce de suivre de près les standards émergents de Java. Cette démarche permet de tirer parti des fonctionnalités les plus récentes offertes par la plateforme Java tout en assurant une transition fluide pour les développeurs. 

Spring n’expose pas publiquement de roadmap ou de programme de planification comme Trello, cependant il y a des orientations et des plans de développement pour les versions futures qui sont discutés au sein de la communauté. Les discussions sur les fonctionnalités à venir, les améliorations et les changements majeurs peuvent avoir lieu sur les forums de discussion, les listes de diffusion, et les issues sur GitHub.

### Gestion de Code Source 

L’outil pour la gestion du Code Source des différents modules de Spring s’appuie sur GitHub, facilitant le travail d’équipe et le suivi des modifications apportés au code. 

Les branches sont nommées en fonction de la version du projet, respectant le Release Pattern. Tant que la branche est supportée celle-ci reçoit des modifications régulières, principalement l’ajout de petites fonctionnalités et des correctifs, en utilisant du rétroportage, consistant à récupérer une nouvelle modification et le déployer dans une ancienne version du service. Une fois que la version n’est plus prise en charge, la branche est clôturée empêchant de nouvelles modifications. 

On retrouve également d’autres branches, comme `docs-build`, une branche dédiée à la construction de la documentation. La branche `main` contient la version la plus récente du projet. 

On retrouve l’utilisation de tag et d’assignation de tâches dans les issues.

### Build Automatisé

La gestion du processus de build automatisé dans le cadre des modules de Spring repose sur l'utilisation d'un bot effectuant des workflows, des processus automatisés qui permettent une intégration continue et un déploiement régulier. Ces workflows automatisés garantissent une gestion fluide du cycle de vie du logiciel, de la compilation à la génération de la documentation. 

L’outil de build privilégié par Spring est Gradle. L'utilisation de scripts Gradle simplifie la définition des dépendances, des plugins et des actions spécifiques au build, facilitant ainsi la maintenance et l'évolution des modules. 

Le support de JUnit5 est intégré au processus de build automatisé. Cela permet l'exécution de tests unitaires de manière systématique à chaque modification, permettant d’identifier rapidement d’éventuels problèmes dans les modifications récentes. D’autres dépendances telles que Mockito et AssertJ sont incluses dans le build, offrant des outils supplémentaires pour les tests automatisés. 

Le processus de build est configuré pour inclure des liens vers diverses documentations Javadoc externes pour faciliter la génération de la documentation. Ces liens incluent des sources telles qu'Oracle JDK, Jakarta EE, IBM WebSphere, Hibernate, Jackson et d'autres.

### Intégration Continue (CI) 

Pour la partie Intégration Continue, Spring utilise Concourses facilitant la construction automatisée. On peut retrouver une instance dédiée de Concourses accessible [ici](https://ci.spring.io). 

Au cœur de ce processus se trouve le fichier `pipeline.yml` qui répertorie les ressources Concourses, c’est-à-dire les entrées et sorties de la construction comme les images de conteneurs, dépôts d'artefacts et de source, etc. Il décrit également les "jobs", soit une séquence d'entrées, de tâches et de sorties orchestrant ainsi le flux de travail de la construction automatisée. Les jobs sont regroupés par groupe (cf. Image ci-dessous pour le module Framework).

![builds](https://github.com/louisc-un/ASE-analyse-devops-Spring/blob/main/builds.png)

![releases](https://github.com/louisc-un/ASE-analyse-devops-Spring/blob/main/releases.png)

![ci-images](https://github.com/louisc-un/ASE-analyse-devops-Spring/blob/main/ci-images.png)

### Analyse de Code et Sécurité

Pour éviter de divulguer publiquement les vulnérabilités de sécurité, Spring encourage les utilisateurs qui identifient un problème à envoyer un e-mail afin que la situation puisse être traitée en interne. 

Les employés de VMware sont responsables de la gestion des pull requests et effectuent des peer-reviews avant de fusionner du code.

### Documentation

Spring propose une documentation complète couvrant une gamme diversifiée de sujets. Celle-ci est retrouvable [ici](https://docs.spring.io/spring-framework/reference/index.html).

### Lean management 

Spring adopte les méthodes agiles dans leur processus de travail, permettant aux clients de participer tout au long de l'avancement d'un projet. Cette méthode a pour objectif de livrer rapidement des fonctionnalités et d'ajuster facilement des modifications en fonction des retours continus. L'équipe Spring partage de manière récurrente leurs connaissances et expériences en matière de méthodes agiles et DevOps à travers leur blog offrant une ressource supplémentaire à la communauté cherchant à appliquer ces concepts.

## Propositions d'améliorations

### Planification et roadmap

Une piste d'amélioration qui permettrait une meilleure transparence sur la gestion des tâches et la vision future du projet serait de rendre public leur tableau Kanban et de fournir une roadmap de leur planification de projet. De cette manière, les développeurs externes et utilisateurs du projet peuvent avoir un meilleur aperçu global de l’avancement de la release et aider au mieux au développement s’ils le souhaitent. Sans cela, il est difficile de savoir quelles tâches ont été réalisées récemment, celles sur lesquelles les efforts sont placés actuellement et celles qui sont prévues dans le futur. 

### Les tests 

Une autre amélioration est de rendre publics les tests dans le cadre du développement des différents modules. La transparence des tests peut offrir aux développeurs externes une meilleure compréhension du fonctionnement du framework et de ses fonctionnalités. Cela favorise également la confiance des utilisateurs, pouvant ainsi développer en se basant sur plus de tests robustes évitant tout problème futur avec certaines features.

# Conclusion

On peut constater au travers de ce document que l’équipe qui est derrière le développement du framework Spring fait utilisation de nombreuses techniques favorisant les bonnes pratiques du DevOps. Celles-ci sont nécessaires pour maintenir le rythme effréné de mise en production qu’a pris ce projet open source utilisé massivement dans le monde de l’entreprise. 

VMware Tanzu a réussi à mettre en place une certaine philosophie derrière le développement de ce framework avec son cadre de travail idéal pour les salariés, mais également en restant transparent et réactif envers la communauté par le biais de blogs, newsletters ou échanges sur internet. 

La force de ce projet réside dans la collaboration de la communauté sur le code source du projet, de sa nature open source, mais également grâce à la mise en application de plusieurs techniques qui accélèrent la vitesse de processus de développement et de mise en production. Les métriques DORA utilisées ici dans le projet en sont les causes principales. On regrette toutefois qu’il n'y ait pas plus d’informations sur la planification du projet comme par exemple une roadmap qui serait rendue disponible ou encore plus de visibilité sur les tests exécutés.

# Ressources 

- https://github.com/spring-projects/spring-framework/blob/6.0.x/build.gradle  

- https://github.com/spring-projects/spring-framework/tree/main/spring-test/src/main/java/org/springframework/test/context  

- https://github.com/spring-projects/spring-framework/blob/6.0.x/ci/README.adoc  

- https://kanoma.fr/blog/concourse-ci/#:~:text=Concourse%20CI%20est%20une%20plateforme,du%20pipeline%20dans%20des%20conteneurs 

- https://tanzu.vmware.com/devops  

- https://tanzu.vmware.com/agile 

- https://content.cdntwrk.com/files/aT0xNDg4NDU1JnY9MiZpc3N1ZU5hbWU9dm13YXJlLXZvaWNlcy1vZi10aGUtdmFuZ3VhcmRzJmNtZD1kJnNpZz1kYTc4ZTJmZDQ3OTY0Y2IzMTUzZDEyMzQ4MDRmMDY1Mg%253D%253D  

- https://tanzu.vmware.com/fr/careers 

- https://content.cdntwrk.com/files/aT0xNDkwNzA0JnY9MiZpc3N1ZU5hbWU9c3RhdGVvZnNwcmluZzIwMjImY21kPWQmc2lnPTRlYzI1Y2UwYzM4ODhiM2JiZGQ0Njk4NWZjY2RmZTZi  

- https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/company/vmw-annual-report-2022.pdf 

- https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/company/vmw-annual-report-2023.pdf 

- https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/microsites/vmware-global-impact-report.pdf 

- https://github.com/spring-projects/spring-framework/pulse/monthly  

- https://status.spring.io/  

- https://github.com/spring-projects/spring-boot/labels?page=1&sort=name-asc 

- https://endoflife.date/spring-framework  

- https://spring.io/projects/spring-framework#support  

- https://github.com/spring-projects/spring-framework/releases?page=2
