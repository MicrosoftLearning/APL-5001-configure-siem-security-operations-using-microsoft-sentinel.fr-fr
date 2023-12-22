---
lab:
  title: "Exercice\_03\_: Valider le déploiement Sentinel"
  module: 'Guided Project - Configure Microsoft Sentinel Data Collection rules, NRT Analytic rule and Automation'
---

>**Remarque** : ce labo s’appuie sur les Lab 01 et Lab 02. Pour suivre ce labo, vous devez disposer d’un [abonnement Azure](https://azure.microsoft.com/free/?azure-portal=true). pour lequel vous disposez d’un accès administratif.

## Recommandations générales

- Lors de la création d’objets, utilisez les paramètres par défaut, à moins que des exigences ne requièrent des configurations différentes.
- Ne créez, ne supprimez ou ne modifiez des objets que pour répondre aux exigences énoncées. Des modifications inutiles de l’environnement peuvent avoir un effet négatif sur votre score final.
- S’il existe plusieurs approches pour atteindre un objectif, choisissez toujours celle qui nécessite le moins d’efforts administratifs.

Nous devons configurer Microsoft Sentinel pour qu’il reçoive les événements de sécurité des machines virtuelles qui exécutent Windows.

## Diagramme de l'architecture

![Diagramme de Windows Security Events via AMA à l’aide de DCR](../Media/apl-5001-lab-diagrams-lab03.png)

## Tâches d'apprentissage

Vous devez valider le déploiement de Microsoft Sentinel pour qu’il réponde aux exigences suivantes :

- Configurez Windows Security Events via le connecteur AMA pour collecter tous les événements de sécurité provenant uniquement d’une machine virtuelle nommée VM1.
- Créez une règle de requête en temps quasi réel (NRT) pour générer un incident basé sur la requête suivante.

```KQL
SecurityEvent 
| where EventID == 4732
| where TargetAccount == "Builtin\\Administrators"
```

- Créez une règle d’automatisation qui attribue à Operator1 le rôle de propriétaire pour les incidents générés par la règle NRT.

## Instructions de l’exercice

>**Remarque** : dans les tâches suivantes, pour accéder à `Microsoft Sentinel`, sélectionnez le fichier `workspace` que vous avez créé au Lab 01.

### Tâche 1 : Configurer les règles de collecte de données (DCR) dans Microsoft Sentinel

Configurez un Windows Security Events via le connecteur AMA. En savoir plus sur [Windows Security Events via le connecteur AMA](https://learn.microsoft.com/azure/sentinel/data-connectors/windows-security-events-via-ama).

 1. Dans `Microsoft Sentinel`, accédez à la section de menu `Configuration` et sélectionnez **Connecteurs de données**.
 1. Recherchez et sélectionnez **Windows Security Events via AMA**.
 1. Sélectionnez **Ouvrir la page du connecteur**.
 1. Dans la zone `Configuration`, sélectionnez **+Créer une règle de collecte de données**.
 1. Sous l’onglet `Basics` saisissez un `Rule Name`.
 1. Sous l’onglet `Resources`, développez votre abonnement et le groupe de ressources `RG1` dans la colonne `Scope`.
 1. Sélectionnez `VM1`, puis **Suivant : Collecter >**.
 1. Sous l’onglet `Collect`, conservez la valeur par défaut `All Security Events`.
 1. Sélectionnez **Suivant : Vérifier + créer >**, puis **Créer**.

### Tâche 2 : Créer une détection de requête en quasi-temps réel (NRT)

Détectez les menaces avec des règles d’analyse en quasi-temps réel (NRT) dans Microsoft Sentinel. En savoir plus sur les [règles d’analyse NRT dans Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/near-real-time-rules).

 1. Dans `Microsoft Sentinel`, accédez à la section de menu `Configuration` et sélectionnez **Analyses**.
 1. Sélectionnez **+ Créer** et **Règle de requête NRT (préversion)**
 1. Saisissez un `Name` pour la règle, puis sélectionnez **Réaffectation de privilèges** à partir de `Tactics and techniques`.
 1. Sélectionnez **Suivant : Définir la logique de la règle >**.
 1. Entrez la requête KQL dans le `Rule query`formulaire.

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

 1. Sélectionnez **Suivant : Paramètres d’incident >**, puis Sélectionnez **Suivant : Réponse automatisée >**
 1. Sélectionnez **Suivant : Vérifier + créer**
 1. Une fois la validation terminée, sélectionnez **Enregistrer**.

### Tâche 3 : Configurer l’automatisation dans Microsoft Sentinel 

Configurez l’automatisation dans Microsoft Sentinel. En savoir plus sur la [création et l’utilisation des règles d’automatisation de Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/create-manage-use-automation-rules).

 1. Dans `Microsoft Sentinel`, accédez à la section de menu `Configuration` et sélectionnez **Automation**.
 1. Sélectionnez **+ Créer** et Règle d’automatisation.
 1. Entrez un `Automation rule name`, puis sélectionnez **Attribuer un propriétaire** à partir de `Actions`.
 1. Attribuez **Operator1** en tant que propriétaire.
 1. Sélectionnez **Appliquer**
