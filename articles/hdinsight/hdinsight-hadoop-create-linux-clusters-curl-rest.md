---
title: "Criar clusters Hadoop usando a API REST do Azure – Azure | Microsoft Docs"
description: Saiba como criar clusters do HDInsight enviando os modelos do Azure Resource Manager para a API REST do Azure.
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="ab61c-103">Criar clusters do Hadoop usando a API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="ab61c-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="ab61c-104">Saiba como criar um cluster HDInsight usando um modelo do Azure Resource Manager e a API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab61c-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="ab61c-105">A API REST do Azure permite executar operações de gerenciamento de serviços hospedados na plataforma Azure, incluindo a criação de novos recursos, como clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab61c-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab61c-106">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="ab61c-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ab61c-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ab61c-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="ab61c-108">As etapas desse documento usam o utilitário [curl (https://curl.haxx.se/)](https://curl.haxx.se/) para se comunicar com a API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab61c-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="ab61c-109">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="ab61c-109">Create a template</span></span>

<span data-ttu-id="ab61c-110">Os modelos do Azure Resource Manager são documentos JSON que descrevem um **grupo de recursos** e todos os recursos que ele contém (por exemplo, HDInsight). Essa abordagem baseada em modelo permite que você defina os recursos necessários para o HDInsight em um modelo.</span><span class="sxs-lookup"><span data-stu-id="ab61c-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="ab61c-111">O seguinte documento JSON é uma fusão dos arquivos de modelo e parâmetros de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), que cria um cluster baseado em Linux usando uma senha para proteger a conta de usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="ab61c-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="ab61c-112">Esse exemplo será usado nas etapas presentes neste documento.</span><span class="sxs-lookup"><span data-stu-id="ab61c-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="ab61c-113">Substitua os *valores* de exemplo na seção **Parâmetros** pelos valores para o cluster.</span><span class="sxs-lookup"><span data-stu-id="ab61c-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab61c-114">O modelo usa o número padrão de nós de trabalho (4) para um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab61c-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="ab61c-115">Se você planeja ter mais de 32 nós de trabalho, será necessário selecionar um tamanho de nó de cabeçalho com pelo menos 8 núcleos e 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="ab61c-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="ab61c-116">Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ab61c-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="ab61c-117">Entre na sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="ab61c-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="ab61c-118">Siga as etapas documentadas em [Introdução à CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) e conecte-se à sua assinatura usando o comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="ab61c-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="ab61c-119">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="ab61c-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="ab61c-120">Essas etapas são uma versão resumida da seção *Criar a entidade de serviço com uma senha* do documento [Usar a CLI do Azure para criar uma entidade de serviço para acessar recursos](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="ab61c-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="ab61c-121">Estas etapas criam uma entidade de serviço que é usada para autenticar a API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab61c-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="ab61c-122">Em uma linha de comando, use o seguinte comando para listar as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab61c-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="ab61c-123">Na lista, selecione a assinatura que você deseja usar e observe as colunas **Subscription_ID** e __Tenant_ID__.</span><span class="sxs-lookup"><span data-stu-id="ab61c-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="ab61c-124">Salve esses valores.</span><span class="sxs-lookup"><span data-stu-id="ab61c-124">Save these values.</span></span>

2. <span data-ttu-id="ab61c-125">Use o comando a seguir para criar um aplicativo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab61c-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="ab61c-126">Substitua os valores de `--display-name`, `--homepage` e `--identifier-uris` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ab61c-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="ab61c-127">Forneça uma senha para a nova entrada do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab61c-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ab61c-128">Os valores `--home-page` e `--identifier-uris` não precisam fazer referência a uma página da Web real hospedada na Internet.</span><span class="sxs-lookup"><span data-stu-id="ab61c-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="ab61c-129">Eles devem ser URIs exclusivos.</span><span class="sxs-lookup"><span data-stu-id="ab61c-129">They must be unique URIs.</span></span>

   <span data-ttu-id="ab61c-130">O valor retornado deste comando é a __ID do aplicativo__ do novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab61c-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="ab61c-131">Salve esse valor.</span><span class="sxs-lookup"><span data-stu-id="ab61c-131">Save this value.</span></span>

3. <span data-ttu-id="ab61c-132">Use o comando a seguir para criar uma entidade de serviço usando a **ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="ab61c-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="ab61c-133">O valor retornado deste comando é a __ID de Objeto__.</span><span class="sxs-lookup"><span data-stu-id="ab61c-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="ab61c-134">Salve esse valor.</span><span class="sxs-lookup"><span data-stu-id="ab61c-134">Save this value.</span></span>

4. <span data-ttu-id="ab61c-135">Atribua a função **Proprietário** à entidade de serviço usando o valor da **ID de Objeto**.</span><span class="sxs-lookup"><span data-stu-id="ab61c-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="ab61c-136">Use o valor **ID da assinatura** obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab61c-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="ab61c-137">Obtenha um token de autenticação</span><span class="sxs-lookup"><span data-stu-id="ab61c-137">Get an authentication token</span></span>

<span data-ttu-id="ab61c-138">Use o seguinte comando para recuperar um token de autenticação:</span><span class="sxs-lookup"><span data-stu-id="ab61c-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="ab61c-139">Defina `$TENANTID`, `$APPID` e `$PASSWORD` para os valores obtidos ou usado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab61c-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="ab61c-140">Se essa solicitação for bem-sucedida, você receberá uma resposta do 200 series, e o corpo da resposta conterá um documento JSON.</span><span class="sxs-lookup"><span data-stu-id="ab61c-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="ab61c-141">O documento JSON retornado por esta solicitação contém um elemento denominado **access_token**.</span><span class="sxs-lookup"><span data-stu-id="ab61c-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="ab61c-142">O valor de **access_token** é usado para solicitações de autenticação para a API REST.</span><span class="sxs-lookup"><span data-stu-id="ab61c-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="ab61c-143">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ab61c-143">Create a resource group</span></span>

<span data-ttu-id="ab61c-144">Use o que é descrito a seguir para criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab61c-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="ab61c-145">Substitua `$SUBSCRIPTIONID` pela ID da assinatura recebida ao criar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="ab61c-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="ab61c-146">Substitua `$ACCESSTOKEN` pelo token de acesso recebido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="ab61c-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="ab61c-147">Substitua `DATACENTERLOCATION` pelo data center no qual você quer criar o grupo de recursos e os recursos.</span><span class="sxs-lookup"><span data-stu-id="ab61c-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="ab61c-148">Por exemplo, "Centro-Sul dos EUA".</span><span class="sxs-lookup"><span data-stu-id="ab61c-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="ab61c-149">Defina `$RESOURCEGROUPNAME` como o nome que deseja usar para este grupo:</span><span class="sxs-lookup"><span data-stu-id="ab61c-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="ab61c-150">Se essa solicitação for bem-sucedida, você receberá uma resposta do 200 series e o corpo da resposta conterá um documento JSON com informações sobre o grupo.</span><span class="sxs-lookup"><span data-stu-id="ab61c-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="ab61c-151">O elemento `"provisioningState"` contém um valor de `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="ab61c-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="ab61c-152">Criar uma implantação</span><span class="sxs-lookup"><span data-stu-id="ab61c-152">Create a deployment</span></span>

<span data-ttu-id="ab61c-153">Execute o comando a seguir para implantar o modelo no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab61c-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="ab61c-154">Defina `$DEPLOYMENTNAME` como o nome que deseja usar para esta implantação.</span><span class="sxs-lookup"><span data-stu-id="ab61c-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="ab61c-155">Se você salvou o modelo em um arquivo, pode usar o seguinte comando em vez de `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="ab61c-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="ab61c-156">Se essa solicitação for bem-sucedida, você receberá uma resposta do 200 series e o corpo da resposta conterá um documento JSON com informações sobre a operação de implantação.</span><span class="sxs-lookup"><span data-stu-id="ab61c-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab61c-157">A implantação foi enviada, mas não foi concluída.</span><span class="sxs-lookup"><span data-stu-id="ab61c-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="ab61c-158">Pode levar vários minutos, normalmente em torno de 15, para concluir a implantação.</span><span class="sxs-lookup"><span data-stu-id="ab61c-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="ab61c-159">Verificar o status de uma implantação</span><span class="sxs-lookup"><span data-stu-id="ab61c-159">Check the status of a deployment</span></span>

<span data-ttu-id="ab61c-160">Para verificar o status da implantação, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab61c-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="ab61c-161">Esse comando retorna informações de um documento JSON que contém informações sobre a operação de implantação.</span><span class="sxs-lookup"><span data-stu-id="ab61c-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="ab61c-162">O elemento `"provisioningState"` contém o status da implantação.</span><span class="sxs-lookup"><span data-stu-id="ab61c-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="ab61c-163">Se esse elemento contiver um valor de `"Succeeded"`, a implantação foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="ab61c-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="ab61c-164">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ab61c-164">Troubleshoot</span></span>

<span data-ttu-id="ab61c-165">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="ab61c-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab61c-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab61c-166">Next steps</span></span>

<span data-ttu-id="ab61c-167">Agora que você criou com êxito um cluster HDInsight, use o seguinte para aprender a trabalhar com o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="ab61c-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="ab61c-168">Clusters do Hadoop</span><span class="sxs-lookup"><span data-stu-id="ab61c-168">Hadoop clusters</span></span>

* [<span data-ttu-id="ab61c-169">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ab61c-170">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ab61c-171">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="ab61c-172">Clusters do HBase</span><span class="sxs-lookup"><span data-stu-id="ab61c-172">HBase clusters</span></span>

* [<span data-ttu-id="ab61c-173">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="ab61c-174">Desenvolvimento de aplicativos Java para HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="ab61c-175">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="ab61c-175">Storm clusters</span></span>

* [<span data-ttu-id="ab61c-176">Desenvolver topologias Java para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ab61c-177">Usar componentes de Python no Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="ab61c-178">Implantar e monitorar topologias com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab61c-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
