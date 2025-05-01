---
lab:
  title: "Exercice\_02\_: Ingérer des données d’événement Sécurité Windows"
  module: Guided Project - Deploy Microsoft Sentinel Content Hub solutions and data connectors
---

>**Remarque** : ce labo s’appuie sur le Lab 01. Pour suivre ce labo, vous devez disposer d’un [abonnement Azure](https://azure.microsoft.com/free/?azure-portal=true). pour lequel vous disposez d’un accès administratif.

## Recommandations générales

- Lors de la création d’objets, utilisez les paramètres par défaut, à moins que des exigences ne requièrent des configurations différentes.
- Ne créez, ne supprimez ou ne modifiez des objets que pour répondre aux exigences énoncées. Des modifications inutiles de l’environnement peuvent avoir un effet négatif sur votre score final.
- S’il existe plusieurs approches pour atteindre un objectif, choisissez toujours celle qui nécessite le moins d’efforts administratifs.

Nous devons configurer Microsoft Sentinel pour ingérer des données en utilisant les solutions Microsoft Sentinel.

## Diagramme de l'architecture

![Diagramme des connecteurs de données Content Hub](../Media/apl-5001-lab-diagrams-lab02.png)

## Tâches d'apprentissage

Vous devez déployer des solutions Content Hub dans l’espace de travail Microsoft Sentinel et répondre aux exigences suivantes :

- Installez les solutions suivantes :
  - Windows Security Events.
  - Connecteur Azure Activity.
  - Microsoft Defender pour le cloud.
- Configurez le connecteur de données pour Azure Activity afin d’appliquer toutes les ressources nouvelles et existantes dans l’abonnement.
- Configurez le connecteur de données de Microsoft Defender pour le cloud pour qu’il se connecte à l’abonnement Azure et assurez-vous que seule la synchronisation bidirectionnelle est activée.
- Activez une règle d’analyse basée sur le modèle Nombre suspect d’activités de création ou de déploiement de ressources. La règle doit être exécutée toutes les heures et ne doit consulter que les données de la dernière heure.
- Assurez-vous que le classeur Activité Azure est disponible dans Mes classeurs.

## Instructions de l’exercice

>**Remarque** : dans les tâches suivantes, pour accéder à `Microsoft Sentinel`, sélectionnez le fichier `workspace` que vous avez créé au Lab 01.

### Tâche 1 : Déployer une solution Microsoft Sentinel Content Hub

Déployez une solution Content Hub et configurez les connecteurs de données. En savoir plus sur les [solutions Content Hub](https://learn.microsoft.com/azure/sentinel/sentinel-solutions).

1. Dans `Microsoft Sentinel`, accédez à la section de menu `Content management` et sélectionnez **Content Hub**.
1. Recherchez et sélectionnez **Windows Security Events**.
1. Sélectionnez le lien pour **afficher les détails**
1. Sélectionnez le plan Windows Security Events, puis **Créer**.
1. Sélectionnez le groupe de ressources `RG2` qui inclut l’espace de travail Microsoft Sentinel, puis sélectionnez le `Workspace`.
1. Sélectionnez **Suivant** dans l’onglet Connecteurs de données (la solution déploiera 2 connecteurs de données).
1. Sélectionnez **Suivant** dans l’onglet Classeurs (la solution installe les classeurs).
1. Sélectionnez **Suivant** dans l’onglet Analyses (la solution installe les règles d’analyse).
1. Sélectionnez **Suivant** dans l’onglet Requêtes de chasse (la solution installe des requêtes de chasse).
1. Sélectionner **Vérifier + créer**
1. Sélectionnez **Créer**

1. Répétez ces étapes pour les solutions `Azure Activity` et les solutions `Microsoft Defender for Cloud`.

### Tâche 2 : Configurer le connecteur de données pour Azure Activity

Configurez le connecteur de données pour Azure Activity afin d’appliquer toutes les ressources nouvelles et existantes dans l’abonnement. En savoir plus sur les [connecteur de données Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/connect-data-sources).

  1. Dans `Microsoft Sentinel`, accédez à la section de menu `Content management` et sélectionnez **Content Hub**.
  1. Dans `Content hub`, filtrez `Status` sur les solutions installées.
  1. Sélectionnez la solution `Azure Activity`, puis sélectionnez **Gérer**.
  1. Sélectionnez le connecteur de données `Azure Activity`, puis la page **Ouvrir le connecteur**.
  1. Dans la zone `Configuration` sous l’onglet `Instructions`, descendez jusqu’à `2. Connect your subscriptions...` et sélectionnez **Lancer l’assistant d’affectation Azure Policy>**.
  1. Sous l’onglet **Informations de base**, sélectionnez le bouton de sélection (…) sous **Étendue**, sélectionnez votre « Abonnement » dans la liste déroulante et cliquez sur **Sélectionner**.
  1. Sélectionnez l’onglet **Paramètres**, choisissez votre espace de travail dans la liste déroulante **Espace de travail Log Analytics principal**.
  1. Sélectionnez l’onglet **Correction** et cochez la case **Créer une tâche de correction**.
  1. Sélectionnez le bouton **Vérifier + créer** pour passer en revue la configuration.
  1. Sélectionnez **Créer** pour terminer.
  
### Tâche 3 : Configurer le connecteur de données Defender pour le cloud

Configurez le connecteur de données pour Microsoft Defender pour le cloud et vérifiez que seule la gestion des incidents est configurée.

  1. Dans `Microsoft Sentinel`, accédez à la section de menu `Content management` et sélectionnez **Content Hub**.
  1. Dans `Content hub`, filtrez `Status` sur les solutions installées.
  1. Sélectionnez la solution `Microsoft Defender for Cloud`, puis sélectionnez **Gérer**.
  1. Sélectionnez le connecteur de données `Subscription-based Microsoft Defender for Cloud (Legacy)`, puis la page **Ouvrir le connecteur**.
  1. Dans la zone `Configuration` sous l’onglet `Instructions`, descendez jusqu’à votre abonnement et placez le curseur dans la colonne `Status` sur **Connecté**.
  1. Vérifiez que `Bi-directional sync` est **activé**.

### Tâche 4 : Créer une règle d’analyse

Créez une règle d’analyse basée sur le modèle Nombre suspect d’activités de création ou de déploiement de ressources. La règle doit être exécutée toutes les heures et ne doit consulter que les données de la dernière heure. En savoir plus sur l’[utilisation des modèles de règles d’analyse Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/detect-threats-built-in).

  1. Dans `Microsoft Sentinel`, accédez à la section de menu `Configuration` et sélectionnez **Analyses**.
  1. Dans l’onglet `Rule templates`, recherchez le **Nombre suspect d’activités de création ou de déploiement de ressources**.
  1. Sélectionnez le **Nombre suspect d’activités de création ou de déploiement de ressources**, puis sélectionnez **Créer une règle**.
  1. Conservez les valeurs par défaut de l’onglet `General` et sélectionnez **Suivant : Définir la logique de la règle >**.
  1. Conservez la valeur par défaut pour `Rule query` et configurez `Query scheduling` à l’aide de la table :

     |Paramètre |Valeur|
     |---|---|
     |Exécuter la requête toutes les|1 heure|
     |Rechercher les données des derniers|1 heure|

  1. Sélectionnez **Suivant : Paramètres d’incident >**.
  1. Conservez les valeurs par défaut et sélectionnez **Suivant : Réponse automatisée >**.
  1. Conservez les valeurs par défaut et sélectionnez **Suivant : Vérifier et créer >**.
  1. Cliquez sur **Enregistrer**.

### Tâche 5 : S’assurer que le classeur Activité Azure est disponible dans Mes classeurs

  1. Dans `Microsoft Sentinel`, accédez à la section de menu `Content management` et sélectionnez **Content Hub**.
  1. Dans `Content hub`, filtrez `Status` sur les solutions installées.
  1. Sélectionnez la solution `Azure Activity`, puis sélectionnez **Gérer**.
  1. Sélectionnez le classeur `Azure Activity` `checkbox`, puis sélectionnez **Configuration**.
  1. Sélectionnez le classeur `Azure Activity`, puis sélectionnez **Enregistrer**.
  1. Choisissez le `Azure Region` pour votre espace de travail `Microsoft Sentinel`.  
