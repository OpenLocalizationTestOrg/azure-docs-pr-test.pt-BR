---
title: clusters de Hadoop aaaCreate usando a API REST do Azure - Azure | Microsoft Docs
description: Saiba como toocreate HDInsight clusters enviando toohello de modelos do Gerenciador de recursos do Azure API REST do Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="54a9d-103">Criar clusters de Hadoop usando Olá API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="54a9d-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="54a9d-104">Saiba como toocreate uma HDInsight cluster usando um modelo do Gerenciador de recursos do Azure e Olá API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="54a9d-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="54a9d-105">Olá API REST do Azure permite operações de gerenciamento de tooperform em serviços hospedados em Olá plataforma Windows Azure, incluindo a criação de saudação de novos recursos, como clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54a9d-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a9d-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="54a9d-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="54a9d-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="54a9d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="54a9d-108">Olá etapas Olá de usar este documento [ondulação (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilitário com hello API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="54a9d-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="54a9d-109">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="54a9d-109">Create a template</span></span>

<span data-ttu-id="54a9d-110">Os modelos do Azure Resource Manager são documentos JSON que descrevem um **grupo de recursos** e todos os recursos que ele contém (por exemplo, HDInsight). Essa abordagem baseada em modelo permite que você os recursos de saudação toodefine que você precisa para HDInsight em um modelo.</span><span class="sxs-lookup"><span data-stu-id="54a9d-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="54a9d-111">Olá documento JSON a seguir é uma fusão de saudação arquivos de modelo e os parâmetros de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), que cria um baseados em Linux cluster usando uma saudação de toosecure de senha SSH conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="54a9d-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="54a9d-112">Este exemplo é usado nas etapas Olá neste documento.</span><span class="sxs-lookup"><span data-stu-id="54a9d-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="54a9d-113">Substitua o exemplo hello *valores* em Olá **parâmetros** seção com valores de saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="54a9d-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a9d-114">modelo de Olá usa o número padrão de saudação de nós de trabalho (4) para um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54a9d-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="54a9d-115">Se você planeja ter mais de 32 nós de trabalho, será necessário selecionar um tamanho de nó de cabeçalho com pelo menos 8 núcleos e 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="54a9d-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="54a9d-116">Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="54a9d-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="54a9d-117">Faça logon no tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="54a9d-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="54a9d-118">Execute as etapas de saudação documentadas em [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) e conecte-se a assinatura de tooyour usando Olá `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="54a9d-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="54a9d-119">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="54a9d-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="54a9d-120">Essas etapas são uma versão resumida do hello *criar entidade de serviço com a senha* seção Olá [toocreate CLI do Azure Use uma entidade de serviço tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) documento.</span><span class="sxs-lookup"><span data-stu-id="54a9d-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="54a9d-121">Essas etapas de criam uma entidade de serviço é usado tooauthenticate toohello API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="54a9d-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="54a9d-122">Em uma linha de comando, use Olá toolist de comando a seguir suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="54a9d-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="54a9d-123">Na lista de hello, selecione a assinatura de saudação que você deseja toouse e observe Olá **Subscription_ID** e __Tenant_ID__ colunas.</span><span class="sxs-lookup"><span data-stu-id="54a9d-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="54a9d-124">Salve esses valores.</span><span class="sxs-lookup"><span data-stu-id="54a9d-124">Save these values.</span></span>

2. <span data-ttu-id="54a9d-125">Use Olá comando toocreate um aplicativo no Azure Active Directory a seguir.</span><span class="sxs-lookup"><span data-stu-id="54a9d-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="54a9d-126">Substituir valores Olá Olá `--display-name`, `--homepage`, e `--identifier-uris` com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="54a9d-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="54a9d-127">Forneça uma senha para a nova entrada de Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="54a9d-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54a9d-128">Olá `--home-page` e `--identifier-uris` valores não é necessário tooreference uma página da web hospedado em Olá internet.</span><span class="sxs-lookup"><span data-stu-id="54a9d-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="54a9d-129">Eles devem ser URIs exclusivos.</span><span class="sxs-lookup"><span data-stu-id="54a9d-129">They must be unique URIs.</span></span>

   <span data-ttu-id="54a9d-130">valor retornado deste comando Hello é hello __ID do aplicativo__ para o novo aplicativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54a9d-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="54a9d-131">Salve esse valor.</span><span class="sxs-lookup"><span data-stu-id="54a9d-131">Save this value.</span></span>

3. <span data-ttu-id="54a9d-132">Comando de uso a seguir de Olá toocreate uma entidade de serviço usando Olá **ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="54a9d-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="54a9d-133">valor retornado deste comando Hello é hello __ID de objeto__.</span><span class="sxs-lookup"><span data-stu-id="54a9d-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="54a9d-134">Salve esse valor.</span><span class="sxs-lookup"><span data-stu-id="54a9d-134">Save this value.</span></span>

4. <span data-ttu-id="54a9d-135">Atribuir Olá **proprietário** entidade de serviço toohello de função usando Olá **ID de objeto** valor.</span><span class="sxs-lookup"><span data-stu-id="54a9d-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="54a9d-136">Saudação de uso **ID da assinatura** obtidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="54a9d-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="54a9d-137">Obtenha um token de autenticação</span><span class="sxs-lookup"><span data-stu-id="54a9d-137">Get an authentication token</span></span>

<span data-ttu-id="54a9d-138">Use Olá comando tooretrieve um token de autenticação a seguir:</span><span class="sxs-lookup"><span data-stu-id="54a9d-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="54a9d-139">Definir `$TENANTID`, `$APPID`, e `$PASSWORD` toohello valores obtido ou usado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="54a9d-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="54a9d-140">Se essa solicitação tiver êxito, você receberá uma resposta 200 série e corpo da resposta Olá contém um documento JSON.</span><span class="sxs-lookup"><span data-stu-id="54a9d-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="54a9d-141">documento JSON retornado por esta solicitação Hello contém um elemento denominado **access_token**.</span><span class="sxs-lookup"><span data-stu-id="54a9d-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="54a9d-142">Olá valor **access_token** é usado tooauthentication solicitações toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="54a9d-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="54a9d-143">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="54a9d-143">Create a resource group</span></span>

<span data-ttu-id="54a9d-144">Use Olá toocreate um grupo de recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="54a9d-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="54a9d-145">Definir `$SUBSCRIPTIONID` ID da assinatura toohello recebido durante a criação de saudação entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="54a9d-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="54a9d-146">Definir `$ACCESSTOKEN` toohello token de acesso recebido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="54a9d-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="54a9d-147">Substituir `DATACENTERLOCATION` com o Centro de dados Olá desejar toocreate grupo de recursos de saudação e recursos, em.</span><span class="sxs-lookup"><span data-stu-id="54a9d-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="54a9d-148">Por exemplo, "Centro-Sul dos EUA".</span><span class="sxs-lookup"><span data-stu-id="54a9d-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="54a9d-149">Definir `$RESOURCEGROUPNAME` toohello nome você deseja toouse para este grupo:</span><span class="sxs-lookup"><span data-stu-id="54a9d-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="54a9d-150">Se essa solicitação tiver êxito, você receberá uma resposta 200 série e corpo da resposta Olá contém um documento JSON que contém informações sobre o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54a9d-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="54a9d-151">Olá `"provisioningState"` elemento contém um valor de `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="54a9d-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="54a9d-152">Criar uma implantação</span><span class="sxs-lookup"><span data-stu-id="54a9d-152">Create a deployment</span></span>

<span data-ttu-id="54a9d-153">Saudação de usar o grupo de recursos do comando toodeploy Olá modelo toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="54a9d-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="54a9d-154">Definir `$DEPLOYMENTNAME` toohello nome você deseja toouse para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="54a9d-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="54a9d-155">Se você salvou o arquivo de tooa Olá modelo, você pode usar Olá seguinte comando em vez de `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="54a9d-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="54a9d-156">Se essa solicitação tiver êxito, você receberá uma resposta 200 série e corpo da resposta Olá contém um documento JSON que contém informações sobre a operação de implantação hello.</span><span class="sxs-lookup"><span data-stu-id="54a9d-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a9d-157">implantação de saudação foi enviada, mas não foi concluída.</span><span class="sxs-lookup"><span data-stu-id="54a9d-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="54a9d-158">Pode levar vários minutos, normalmente em torno 15, para Olá toocomplete de implantação.</span><span class="sxs-lookup"><span data-stu-id="54a9d-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="54a9d-159">Verificar o status de uma implantação Olá</span><span class="sxs-lookup"><span data-stu-id="54a9d-159">Check hello status of a deployment</span></span>

<span data-ttu-id="54a9d-160">status de saudação toocheck de implantação de hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="54a9d-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="54a9d-161">Esse comando retorna um documento JSON que contém informações sobre a operação de implantação hello.</span><span class="sxs-lookup"><span data-stu-id="54a9d-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="54a9d-162">Olá `"provisioningState"` elemento contém o status de saudação de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="54a9d-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="54a9d-163">Se esse elemento contém um valor de `"Succeeded"`, em seguida, implantação de saudação foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="54a9d-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="54a9d-164">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="54a9d-164">Troubleshoot</span></span>

<span data-ttu-id="54a9d-165">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="54a9d-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54a9d-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54a9d-166">Next steps</span></span>

<span data-ttu-id="54a9d-167">Agora que você criou com êxito um cluster HDInsight, usar Olá toolearn a seguir como toowork com o cluster.</span><span class="sxs-lookup"><span data-stu-id="54a9d-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="54a9d-168">Clusters do Hadoop</span><span class="sxs-lookup"><span data-stu-id="54a9d-168">Hadoop clusters</span></span>

* [<span data-ttu-id="54a9d-169">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="54a9d-170">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="54a9d-171">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="54a9d-172">Clusters do HBase</span><span class="sxs-lookup"><span data-stu-id="54a9d-172">HBase clusters</span></span>

* [<span data-ttu-id="54a9d-173">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="54a9d-174">Desenvolvimento de aplicativos Java para HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="54a9d-175">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="54a9d-175">Storm clusters</span></span>

* [<span data-ttu-id="54a9d-176">Desenvolver topologias Java para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="54a9d-177">Usar componentes de Python no Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="54a9d-178">Implantar e monitorar topologias com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54a9d-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
