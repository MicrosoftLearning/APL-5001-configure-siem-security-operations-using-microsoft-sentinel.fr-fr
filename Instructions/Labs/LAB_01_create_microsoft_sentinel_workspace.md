---
lab:
  title: "Exercice\_01\_: Déployer Microsoft Sentinel"
  module: Guided Project - Create and configure a Microsoft Sentinel workspace
---

>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure](https://azure.microsoft.com/en-us/free/?azure-portal=true) pour lequel vous disposez d’un accès administratif.

## Recommandations générales

- Lors de la création d’objets, utilisez les paramètres par défaut, à moins que des exigences ne requièrent des configurations différentes.
- Ne créez, ne supprimez ou ne modifiez des objets que pour répondre aux exigences énoncées. Des modifications inutiles de l’environnement peuvent avoir un effet négatif sur votre score final.
- S’il existe plusieurs approches pour atteindre un objectif, choisissez toujours celle qui nécessite le moins d’efforts administratifs.

Nous évaluons actuellement le niveau de sécurité existant de notre environnement d’entreprise. Nous avons besoin de votre aide pour configurer une solution SIEM (Gestion des informations et des événements de sécurité) pour identifier les cyber-attaques futures et en cours.

## Diagramme de l'architecture

![Diagramme avec l’espace de travail Log Analytics.](../Media/apl-5001-lab-diagrams-01.png)

## Tâches d'apprentissage

Vous devez déployer un espace de travail Microsoft Sentinel. La solution doit remplir les conditions suivantes :

- Veillez à ce que les données Sentinel soient stockées dans la région Azure USA Ouest.
- Assurez-vous que tous les journaux d’activité Sentinel sont conservés pendant 180 jours.
- Attribuez des rôles à Operator1 pour qu’il puisse gérer les incidents et exécuter les playbooks Sentinel. La solution doit respecter le principe du privilège minimum.

## Instructions de l’exercice

### Tâche 1 : Créer un espace de travail Log Analytics

Créez un espace de travail Log Analytics, y compris l’option de région. En savoir plus sur l’[intégration Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/quickstart-onboard).

  1. Dans le portail Azure, recherchez et sélectionnez `Microsoft Sentinel`.
  1. Sélectionnez **+ Créer**.
  1. Sélectionnez **Créer un espace de travail**.
  1. Sélectionnez `RG2` comme groupe de ressources.
  1. Saisissez un nom valide pour l’espace de travail Log Analytics.
  1. Sélectionnez `West US` comme la région de l’espace de travail.
  1. Sélectionnez **Vérifier + créer** pour valider le nouvel espace de travail.
  1. Sélectionnez **Créer** pour déployer l’espace de travail.

### Tâche 2 : Déployer Microsoft Sentinel dans un espace de travail

Déployez Microsoft Sentinel dans l’espace de travail.

  1. Une fois le déploiement `workspace` terminé, sélectionnez **Actualiser** pour afficher le nouveau `workspace`.
  1. Sélectionnez l’élément `workspace` auquel vous souhaitez ajouter Sentinel (créé dans la tâche 1).
  1. Sélectionnez **Ajouter**.

### Tâche 3 : Attribuer un rôle Microsoft Sentinel à un utilisateur

Attribuer un rôle Microsoft Sentinel à une utilisation. En savoir plus sur les [rôles et autorisations pour travailler dans Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/roles).

  1. Accédez au groupe de ressources RG2.
  1. Sélectionnez **Contrôle d’accès (IAM)** .
  1. Sélectionnez **Ajouter** et `Add role assignment`.
  1. Dans la barre de recherche, recherchez et sélectionnez le rôle `Microsoft Sentinel Contributor`.
  1. Cliquez sur **Suivant**.
  1. Sélectionnez l’option `User, group, or service principal`.
  1. Sélectionnez **+ Sélectionner des membres**.
  1. Recherchez le `Operator1` attribué dans vos instructions de labo `(operator1-XXXXXXXXX@LODSPRODMCA.onmicrosoft.com)`.
  1. Sélectionnez `user icon`.
  1. Cliquez sur **Sélectionner**.
  1. Sélectionnez « Vérifier + attribuer ».
  1. Sélectionnez « Vérifier + attribuer ».

### Tâche 4 : Configurer la rétention des données

Configurez la rétention des données [En savoir plus sur la rétention des données](https://learn.microsoft.com/azure/azure-monitor/logs/data-retention-archive).

  1. Accédez à `Log Analytics workspace` créé à l’étape 5 de la tâche 1.
  1. Sélectionnez **Utilisation et estimation des coûts**.
  1. Sélectionnez **Rétention des données**.
  1. Modifiez la période de rétention en la portant à **180 jours**.
  1. Cliquez sur **OK**.

>**Remarque** : pour des exercices supplémentaires, suivez le module [Créer et gérer des espaces de travail Microsoft Sentinel](https://learn.microsoft.com/training/modules/create-manage-azure-sentinel-workspaces/).
