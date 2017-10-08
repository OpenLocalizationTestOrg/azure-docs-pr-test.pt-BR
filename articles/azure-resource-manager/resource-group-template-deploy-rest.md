---
title: recursos de aaaDeploy com API REST e o modelo | Microsoft Docs
description: "Use toodeploy um tooAzure de recursos de Gerenciador de recursos do Azure e API de REST do Gerenciador de recursos. Olá recursos são definidos em um modelo do Gerenciador de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Implantar recursos com modelos do Resource Manager e a API REST do Resource Manager
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI do Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Este artigo explica como toouse Olá REST API do Gerenciador de recursos com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos.  

> [!TIP]
> Para obter ajuda com a depuração de erros durante a implantação, consulte:
> 
> * [Exibir operações de implantação](resource-manager-deployment-operations.md) toolearn sobre a obtenção de informações que ajudam você a solucionar o erro
> * [Solucionar erros comuns ao implantar recursos tooAzure com o Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn como tooresolve erros comuns de implantação
> 
> 

Seu modelo pode ser um arquivo local ou um arquivo externo que está disponível por meio de um URI. Quando o modelo estiver em uma conta de armazenamento, você pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso compartilhado durante a implantação.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Implantar com hello API REST
1. Definir [Parâmetros e cabeçalhos comuns](https://docs.microsoft.com/rest/api/index), incluindo tokens de autenticação.
2. Se você não tiver um grupo de recursos existente, crie um grupo de recursos. Forneça seu ID de assinatura, o nome de saudação do novo grupo de recursos hello e local que você precisa para sua solução. Para obter mais informações, consulte [Criar um grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Validar sua implantação antes de executá-lo executando Olá [validar uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operação. Ao testar a implantação de hello, forneça parâmetros exatamente como faria ao executar implantação hello (mostrada na próxima etapa do hello).
4. Crie uma implantação. Fornece sua ID de assinatura, nome Olá Olá do grupo de recursos, nome de saudação da implantação de saudação e um modelo de tooyour de link. Para obter informações sobre o arquivo de modelo hello, consulte [arquivo de parâmetro](#parameter-file). Para obter mais informações sobre a API REST de saudação toocreate um grupo de recursos, consulte [criar uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Saudação de aviso **modo** está definido muito**Incremental**. toorun uma implantação completa, defina **modo** muito**concluir**. Tenha cuidado ao usar o modo completo Olá inadvertidamente, você pode excluir recursos que não estão no modelo.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Se desejar que o conteúdo da resposta toolog, conteúdo da solicitação ou ambos, incluir **debugSetting** na solicitação de saudação.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Você pode configurar seu toouse de conta de armazenamento um token de acesso compartilhado (SAS) de assinatura. Para obter mais informações, consulte [Delegando Acesso com uma Assinatura de Acesso Compartilhado](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Obter status de saudação da implantação de modelo hello. Para obter mais informações, consulte [obter informações sobre uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Arquivo de parâmetro.

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como lidar com operações assíncronas de REST, consulte [controlar operações assíncronas de Azure](resource-manager-async-operations.md).
* Para obter um exemplo de implantação de recursos por meio da biblioteca de cliente .NET hello, consulte [implantar recursos usando as bibliotecas .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).
* Para obter orientação sobre a implantação de ambientes de toodifferent sua solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](solution-dev-test-environments.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

