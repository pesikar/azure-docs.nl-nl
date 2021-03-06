---
title: Azure Red Hat open Shift v4. x configureren met Azure Monitor voor containers | Microsoft Docs
description: In dit artikel wordt beschreven hoe u bewaking configureert voor een Kubernetes-cluster met Azure Monitor dat wordt gehost op Azure Red Hat open Shift versie 4 of hoger.
ms.topic: conceptual
ms.date: 06/30/2020
ms.openlocfilehash: 8cd551a028f2fc67c26f8e32d59c0e0650aa1e54
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/28/2021
ms.locfileid: "98944533"
---
# <a name="configure-azure-red-hat-openshift-v4x-with-azure-monitor-for-containers"></a>Azure Red Hat open Shift v4. x configureren met Azure Monitor voor containers

Azure Monitor voor containers biedt een uitgebreide bewakings ervaring voor Azure Kubernetes service (AKS) en AKS-engine clusters. In dit artikel wordt beschreven hoe u een vergelijk bare bewakings ervaring kunt krijgen door bewaking in te scha kelen voor Kubernetes-clusters die worden gehost op [Azure Red Hat open Shift](../../openshift/intro-openshift.md) versie 4. x.

>[!NOTE]
>De ondersteuning voor Azure Red Hat open Shift is op dit moment een functie in Public Preview.
>

U kunt Azure Monitor voor containers inschakelen voor een of meer bestaande implementaties van Azure Red Hat open Shift v4. x door gebruik te maken van de ondersteunde methoden die in dit artikel worden beschreven.

Voer voor een bestaand cluster dit [bash-script uit in de Azure cli](/cli/azure/openshift#az-openshift-create&preserve-view=true).

## <a name="supported-and-unsupported-features"></a>Ondersteunde en niet-ondersteunde functies

Azure Monitor voor containers ondersteunt de bewaking van Azure Red Hat open Shift v4. x, zoals beschreven in [Azure monitor voor containers Overview](container-insights-overview.md), met uitzonde ring van de volgende functies:

- Live-gegevens (preview-versie)
- [Metrische gegevens verzamelen](container-insights-update-metrics.md) van cluster knooppunten en peulen en deze opslaan in de data base met Azure monitor gegevens

## <a name="prerequisites"></a>Vereisten

- De Azure CLI-versie 2.0.72 of hoger  

- Het [helm 3](https://helm.sh/docs/intro/install/) cli-hulp programma

- [Bash-versie 4](https://www.gnu.org/software/bash/)

- Het opdracht regel programma [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

- Een [Log Analytics-werkruimte](../platform/design-logs-deployment.md).

    Azure Monitor voor containers ondersteunt een Log Analytics-werk ruimte in de regio's die worden vermeld in azure- [producten per regio](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=monitor). Om uw eigen werk ruimte te maken, kan deze worden gemaakt via [Azure Resource Manager](../samples/resource-manager-workspace.md), via [Power shell](../scripts/powershell-sample-create-workspace.md?toc=%2fpowershell%2fmodule%2ftoc.json)of in de [Azure Portal](../learn/quick-create-workspace.md).

- Als u de functies in Azure Monitor voor containers wilt inschakelen en gebruiken, moet u Mini maal een rol voor Azure- *Inzender* hebben in het Azure-abonnement en een rol [*log Analytics inzender*](../platform/manage-access.md#manage-access-using-azure-permissions) in de log Analytics-werk ruimte, geconfigureerd met Azure monitor voor containers.

- Als u de bewakings gegevens wilt bekijken, moet u de rol van [*log Analytics lezer*](../platform/manage-access.md#manage-access-using-azure-permissions) hebben in de log Analytics-werk ruimte, geconfigureerd met Azure monitor voor containers.

## <a name="enable-monitoring-for-an-existing-cluster"></a>Bewaking inschakelen voor een bestaand cluster

Ga als volgt te werk om bewaking in te scha kelen voor een Azure Red Hat open Shift versie 4 of hoger-cluster dat is geïmplementeerd in azure met behulp van het meegeleverde bash-script:

1. Meld u aan bij Azure door de volgende opdracht uit te voeren:

    ```azurecli
    az login
    ```

1. Down load en sla dit op in een lokale map het script waarmee uw cluster wordt geconfigureerd met de invoeg toepassing voor bewaking door de volgende opdracht uit te voeren:

    `curl -o enable-monitoring.sh -L https://aka.ms/enable-monitoring-bash-script`

1. Voer de volgende opdrachten uit om de *kubeContext* van uw cluster te identificeren

    ```
    adminUserName=$(az aro list-credentials -g $clusterResourceGroup -n $clusterName --query 'kubeadminUsername' -o tsv)
    adminPassword=$(az aro list-credentials -g $clusterResourceGroup -n $clusterName --query 'kubeadminPassword' -o tsv)
    apiServer=$(az aro show -g $clusterResourceGroup -n $clusterName --query apiserverProfile.url -o tsv)
    oc login $apiServer -u $adminUserName -p $adminPassword
    # openshift project name for azure monitor for containers
    openshiftProjectName="azure-monitor-for-containers"
    oc new-project $openshiftProjectName
    # get the kube config context
    kubeContext=$(oc config current-context)
    ```

1. Kopieer de waarde voor later gebruik.

### <a name="integrate-with-an-existing-workspace"></a>Integreren met een bestaande werk ruimte

In deze sectie schakelt u de bewaking van uw cluster in met behulp van het bash-script dat u eerder hebt gedownload. Als u wilt integreren met een bestaande Log Analytics-werk ruimte, moet u beginnen met het identificeren van de volledige Resource-ID van uw Log Analytics werk ruimte die is vereist voor de `logAnalyticsWorkspaceResourceId` para meter, en voert u de opdracht uit om de invoeg toepassing voor bewaking in te scha kelen met de opgegeven werk ruimte.

Als u geen werk ruimte hebt om op te geven, kunt u door gaan naar de sectie de [standaard werkruimte integreren](#integrate-with-the-default-workspace) en het script een nieuwe werk ruimte laten maken.

1. Een lijst met alle abonnementen waartoe u toegang hebt door de volgende opdracht uit te voeren:

    ```azurecli
    az account list --all -o table
    ```

    De uitvoer ziet er als volgt uit:

    ```azurecli
    Name                                  CloudName    SubscriptionId                        State    IsDefault
    ------------------------------------  -----------  ------------------------------------  -------  -----------
    Microsoft Azure                       AzureCloud   0fb60ef2-03cc-4290-b595-e71108e8f4ce  Enabled  True
    ```

1. Kopieer de waarde voor **SubscriptionId**.

1. Ga naar het abonnement dat als host fungeert voor de Log Analytics-werk ruimte door de volgende opdracht uit te voeren:

    ```azurecli
    az account set -s <subscriptionId of the workspace>
    ```

1. De lijst met werk ruimten in uw abonnementen weer geven in de standaard JSON-indeling door de volgende opdracht uit te voeren:

    ```
    az resource list --resource-type Microsoft.OperationalInsights/workspaces -o json
    ```

1. Zoek in de uitvoer de naam van de werk ruimte en kopieer de volledige Resource-ID van die Log Analytics werk ruimte onder de veld **-id**.

1. Voer de volgende opdracht uit om controle in te scha kelen. Vervang de waarden voor de `azureAroV4ClusterResourceId` `logAnalyticsWorkspaceResourceId` `kubeContext` para meters, en.

    ```bash
    export azureAroV4ClusterResourceId=“/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.RedHatOpenShift/OpenShiftClusters/<clusterName>”
    export logAnalyticsWorkspaceResourceId=“/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/microsoft.operationalinsights/workspaces/<workspaceName>”
    export kubeContext="<kubeContext name of your ARO v4 cluster>"  
    ```

    Voorbeeld:

    `bash enable-monitoring.sh --resource-id $azureAroV4ClusterResourceId --kube-context $kubeContext --workspace-id $logAnalyticsWorkspaceResourceId`

Nadat u bewaking hebt ingeschakeld, kan het ongeveer 15 minuten duren voordat u de metrische gegevens voor de status voor het cluster kunt weer geven.

### <a name="integrate-with-the-default-workspace"></a>Integreren met de standaardwerk ruimte

In deze sectie schakelt u bewaking in voor uw Azure Red Hat open Shift v4. x-cluster met behulp van het bash-script dat u hebt gedownload.

In dit voor beeld bent u niet verplicht een bestaande werk ruimte vooraf te maken of op te geven. Met deze opdracht vereenvoudigt u het proces voor u door een standaardwerk ruimte te maken in de standaard resource groep van het cluster abonnement als er nog geen bestaat in de regio.

De standaardwerk ruimte die wordt gemaakt, heeft de indeling *DefaultWorkspace- \<GUID> - \<Region>*.  

Vervang de waarden voor de `azureAroV4ClusterResourceId` `kubeContext` para meters en.

```bash
export azureAroV4ClusterResourceId="/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.RedHatOpenShift/OpenShiftClusters/<clusterName>"
export kubeContext="<kubeContext name of your ARO v4 cluster>"
```

Bijvoorbeeld:

`bash enable-monitoring.sh --resource-id $azureAroV4ClusterResourceId --kube-context $kubeContext`

Nadat u bewaking hebt ingeschakeld, kan het ongeveer 15 minuten duren voordat u de metrische gegevens van de status voor het cluster kunt weer geven.

### <a name="enable-monitoring-from-the-azure-portal"></a>Bewaking van de Azure Portal inschakelen

In de weer gave met meerdere clusters in Azure Monitor voor containers worden uw Azure Red Hat open Shift-clusters gemarkeerd waarvoor geen bewaking is ingeschakeld op het tabblad niet- **bewaakte clusters** . De optie **inschakelen** naast het cluster initieert geen controle van de bewaking vanuit de portal. U wordt omgeleid naar dit artikel om de bewaking hand matig in te scha kelen door de stappen te volgen die eerder in dit artikel zijn beschreven.

1. Meld u aan bij [Azure Portal](https://portal.azure.com).

1. Selecteer **Azure monitor** in het linkerdeel venster of op de start pagina.

1. Selecteer in de sectie **inzichten** de optie **containers**.

1. Selecteer op de pagina **monitor-containers** de optie niet- **bewaakte clusters**.

1. Selecteer in de lijst met niet-bewaakte clusters het cluster en selecteer vervolgens **inschakelen**.

    U kunt de resultaten in de lijst identificeren door te zoeken naar de waarde **Aro** in de kolom **cluster type** . Nadat u **inschakelen** hebt geselecteerd, wordt u omgeleid naar dit artikel.

## <a name="next-steps"></a>Volgende stappen

- Nu u bewaking hebt ingeschakeld om het status-en resource gebruik van uw RedHat open Shift versie 4. x-cluster en de werk belastingen die erop worden uitgevoerd te verzamelen, leert u hoe u Azure Monitor voor containers [kunt gebruiken](container-insights-analyze.md) .

- De container agent verzamelt standaard de container-logboeken *stdout* en *stderr* van alle containers die worden uitgevoerd in alle naam ruimten, met uitzonde ring van uitvoeren-System. Als u een container logboek verzameling wilt configureren die specifiek is voor een bepaalde naam ruimte of naam ruimten, bekijkt u de configuratie van de [container Insights-agent](container-insights-agent-config.md) om de instellingen voor het verzamelen van gegevens te configureren die u wilt instellen voor het configuratie bestand van uw *ConfigMap* .

- Als u Prometheus-metrische gegevens uit uw cluster wilt opwaarderen en analyseren, raadpleegt u [Prometheus metrische gegevens uitval configureren](container-insights-prometheus-integration.md).

- Zie [het bewaken van uw Azure Red Hat open Shift-cluster stoppen](./container-insights-optout-openshift-v3.md)als u meer wilt weten over het stoppen van het bewaken van uw cluster met behulp van Azure monitor voor containers.
