---
title: aaaProvision um Cache Redis usando o Gerenciador de recursos do Azure | Microsoft Docs
description: Use o Gerenciador de recursos do Azure modelo toodeploy um Cache Redis do Azure.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Criar um Cache Redis usando um modelo
Neste tópico, você aprenderá como toocreate um modelo do Gerenciador de recursos do Azure que implanta um Azure Redis Cache. cache de saudação pode ser usado com armazenamento conta tookeep diagnóstico dados existentes. Você também aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.

Atualmente, as configurações de diagnóstico são compartilhadas para todos os caches em Olá mesma região para uma assinatura. A atualização de um cache na região Olá afeta todos os outros caches na região de saudação.

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Para o modelo do hello completa, consulte [Redis Cache modelo](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Modelos do Gerenciador de recursos para Olá novo [camada Premium](cache-premium-tier-intro.md) estão disponíveis. 
> 
> * [Criar um cache Redis Premium com clustering](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Criar um cache Redis Premium com persistência de dados](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Criar um cache Redis Premium com VNet e clustering opcional](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck para os modelos mais recentes do hello, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) e procure `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>O que você implantará
Neste modelo, você implantará um Cache Redis do Azure que usa uma conta de armazenamento existente para os dados de diagnóstico.

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros
No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada parâmetros que contém todos os valores de parâmetro hello.
Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores que permanecem sempre Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
local de saudação do hello Cache Redis. Para melhor desempenho, use Olá mesmo local como Olá toobe aplicativo usado com o cache de saudação.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
nome de saudação do Olá existente toouse de conta de armazenamento para diagnóstico. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>enableNonSslPort
Um valor booliano que indica se tooallow acessar por meio de portas não SSL.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Um valor que indica se o diagnóstico está habilitado. Use ATIVAR ou DESATIVAR.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Recursos toodeploy
### <a name="redis-cache"></a>Cache Redis
Cria Olá Cache Redis do Azure.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>CLI do Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


