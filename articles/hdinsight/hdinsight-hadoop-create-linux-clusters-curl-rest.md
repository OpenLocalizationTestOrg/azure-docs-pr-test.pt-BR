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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Criar clusters de Hadoop usando Olá API REST do Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Saiba como toocreate uma HDInsight cluster usando um modelo do Gerenciador de recursos do Azure e Olá API REST do Azure.

Olá API REST do Azure permite operações de gerenciamento de tooperform em serviços hospedados em Olá plataforma Windows Azure, incluindo a criação de saudação de novos recursos, como clusters HDInsight.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!NOTE]
> Olá etapas Olá de usar este documento [ondulação (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilitário com hello API REST do Azure.

## <a name="create-a-template"></a>Criar um modelo

Os modelos do Azure Resource Manager são documentos JSON que descrevem um **grupo de recursos** e todos os recursos que ele contém (por exemplo, HDInsight). Essa abordagem baseada em modelo permite que você os recursos de saudação toodefine que você precisa para HDInsight em um modelo.

Olá documento JSON a seguir é uma fusão de saudação arquivos de modelo e os parâmetros de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), que cria um baseados em Linux cluster usando uma saudação de toosecure de senha SSH conta de usuário.

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

Este exemplo é usado nas etapas Olá neste documento. Substitua o exemplo hello *valores* em Olá **parâmetros** seção com valores de saudação para seu cluster.

> [!IMPORTANT]
> modelo de Olá usa o número padrão de saudação de nós de trabalho (4) para um cluster HDInsight. Se você planeja ter mais de 32 nós de trabalho, será necessário selecionar um tamanho de nó de cabeçalho com pelo menos 8 núcleos e 14 GB de RAM.
>
> Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="log-in-tooyour-azure-subscription"></a>Faça logon no tooyour assinatura do Azure

Execute as etapas de saudação documentadas em [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) e conecte-se a assinatura de tooyour usando Olá `az login` comando.

## <a name="create-a-service-principal"></a>Criar uma entidade de serviço

> [!NOTE]
> Essas etapas são uma versão resumida do hello *criar entidade de serviço com a senha* seção Olá [toocreate CLI do Azure Use uma entidade de serviço tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) documento. Essas etapas de criam uma entidade de serviço é usado tooauthenticate toohello API REST do Azure.

1. Em uma linha de comando, use Olá toolist de comando a seguir suas assinaturas do Azure.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    Na lista de hello, selecione a assinatura de saudação que você deseja toouse e observe Olá **Subscription_ID** e __Tenant_ID__ colunas. Salve esses valores.

2. Use Olá comando toocreate um aplicativo no Azure Active Directory a seguir.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Substituir valores Olá Olá `--display-name`, `--homepage`, e `--identifier-uris` com seus próprios valores. Forneça uma senha para a nova entrada de Active Directory hello.

   > [!NOTE]
   > Olá `--home-page` e `--identifier-uris` valores não é necessário tooreference uma página da web hospedado em Olá internet. Eles devem ser URIs exclusivos.

   valor retornado deste comando Hello é hello __ID do aplicativo__ para o novo aplicativo de saudação. Salve esse valor.

3. Comando de uso a seguir de Olá toocreate uma entidade de serviço usando Olá **ID do aplicativo**.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     valor retornado deste comando Hello é hello __ID de objeto__. Salve esse valor.

4. Atribuir Olá **proprietário** entidade de serviço toohello de função usando Olá **ID de objeto** valor. Saudação de uso **ID da assinatura** obtidos anteriormente.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>Obtenha um token de autenticação

Use Olá comando tooretrieve um token de autenticação a seguir:

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

Definir `$TENANTID`, `$APPID`, e `$PASSWORD` toohello valores obtido ou usado anteriormente.

Se essa solicitação tiver êxito, você receberá uma resposta 200 série e corpo da resposta Olá contém um documento JSON.

documento JSON retornado por esta solicitação Hello contém um elemento denominado **access_token**. Olá valor **access_token** é usado tooauthentication solicitações toohello API REST.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Use Olá toocreate um grupo de recursos a seguir.

* Definir `$SUBSCRIPTIONID` ID da assinatura toohello recebido durante a criação de saudação entidade de serviço.
* Definir `$ACCESSTOKEN` toohello token de acesso recebido na etapa anterior hello.
* Substituir `DATACENTERLOCATION` com o Centro de dados Olá desejar toocreate grupo de recursos de saudação e recursos, em. Por exemplo, "Centro-Sul dos EUA".
* Definir `$RESOURCEGROUPNAME` toohello nome você deseja toouse para este grupo:

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

Se essa solicitação tiver êxito, você receberá uma resposta 200 série e corpo da resposta Olá contém um documento JSON que contém informações sobre o grupo de saudação. Olá `"provisioningState"` elemento contém um valor de `"Succeeded"`.

## <a name="create-a-deployment"></a>Criar uma implantação

Saudação de usar o grupo de recursos do comando toodeploy Olá modelo toohello a seguir.

* Definir `$DEPLOYMENTNAME` toohello nome você deseja toouse para essa implantação.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Se você salvou o arquivo de tooa Olá modelo, você pode usar Olá seguinte comando em vez de `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

Se essa solicitação tiver êxito, você receberá uma resposta 200 série e corpo da resposta Olá contém um documento JSON que contém informações sobre a operação de implantação hello.

> [!IMPORTANT]
> implantação de saudação foi enviada, mas não foi concluída. Pode levar vários minutos, normalmente em torno 15, para Olá toocomplete de implantação.

## <a name="check-hello-status-of-a-deployment"></a>Verificar o status de uma implantação Olá

status de saudação toocheck de implantação de hello, use Olá comando a seguir:

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

Esse comando retorna um documento JSON que contém informações sobre a operação de implantação hello. Olá `"provisioningState"` elemento contém o status de saudação de implantação de saudação. Se esse elemento contém um valor de `"Succeeded"`, em seguida, implantação de saudação foi concluída com êxito.

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas

Agora que você criou com êxito um cluster HDInsight, usar Olá toolearn a seguir como toowork com o cluster.

### <a name="hadoop-clusters"></a>Clusters do Hadoop

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clusters do HBase

* [Introdução ao HBase no HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Desenvolvimento de aplicativos Java para HBase no HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clusters Storm

* [Desenvolver topologias Java para Storm no HDInsight](hdinsight-storm-develop-java-topology.md)
* [Usar componentes de Python no Storm no HDInsight](hdinsight-storm-develop-python-topology.md)
* [Implantar e monitorar topologias com o Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
