---
title: "alterações de tooprevent de recursos do Azure aaaLock | Microsoft Docs"
description: "Impeça que os usuários atualizem ou excluam recursos críticos do Azure ao aplicar um bloqueio a todos os usuários e funções."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Bloquear recursos tooprevent alterações inesperadas 
Como administrador, talvez seja necessário toolock uma assinatura, o grupo de recursos ou o recurso tooprevent outros usuários em sua organização acidentalmente excluir ou modificar recursos críticos. Você pode definir o nível de bloqueio de saudação muito**CanNotDelete** ou **ReadOnly**. 

* **CanNotDelete** significa que os usuários autorizados podem ler e modificar um recurso, mas eles não é possível excluir o recurso de saudação. 
* **ReadOnly** significa que usuários autorizados possam ler um recurso, mas eles não podem excluir ou atualizar o recurso de saudação. Aplicar o bloqueio é semelhante toorestricting todos os autorizados toohello usuários as permissões concedidas pelo Olá **leitor** função. 

## <a name="how-locks-are-applied"></a>Como os bloqueios são aplicados

Quando você aplica um bloqueio em um escopo pai, todos os recursos nesse escopo herdam Olá mesmo bloqueio. Recursos até que você adicionar posteriormente herdam bloqueio de saudação do pai de saudação. bloqueio de Hello mais restritivo em herança Olá terá precedência.

Ao contrário de controle de acesso baseado em função, você pode usar bloqueios de gerenciamento tooapply uma restrição em todos os usuários e funções. toolearn sobre como configurar permissões para usuários e funções, consulte [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).

Bloqueios de Gerenciador de recursos se aplicam somente toooperations que acontecem no plano de gerenciamento hello, que consiste em operações enviadas muito`https://management.azure.com`. bloqueios de saudação não restringem como recursos de executam suas próprias funções. Alterações de recursos são restritas, mas as operações de recursos não são restritas. Por exemplo, um bloqueio de somente leitura em um banco de dados SQL impede a exclusão ou modificação de banco de dados hello, mas ele não impedem que você criar, atualizar ou excluir dados no banco de dados de saudação. Transações de dados são permitidas porque essas operações não são enviadas muito`https://management.azure.com`.

Aplicando **ReadOnly** pode levar a resultados de toounexpected porque algumas operações que parecerem leitura operações realmente exigem ações adicionais. Por exemplo, colocando uma **ReadOnly** bloqueio em uma conta de armazenamento impede que todos os usuários listando chaves hello. lista de saudação operação de chaves é tratada por meio de uma solicitação POST como Olá retornado chaves estão disponíveis para operações de gravação. Outro exemplo, colocando uma **ReadOnly** bloqueio em um recurso de serviço de aplicativo impede que o Visual Studio Server Explorer exibindo arquivos de recurso Olá porque essa interação requer acesso de gravação.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Quem pode criar ou excluir bloqueios na sua organização
bloqueios de gerenciamento toocreate ou delete, você deve ter acesso muito`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações. De saudação funções internas, apenas **proprietário** e **administrador de acesso do usuário** recebem essas ações.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Modelo
Olá, exemplo a seguir mostra um modelo que cria um bloqueio em uma conta de armazenamento. conta de armazenamento Olá no qual tooapply bloqueio Olá é fornecido como um parâmetro. Olá nome do bloqueio de saudação é criado pela concatenação do nome do recurso Olá com **/Microsoft.Authorization/** e Olá nesse caso o nome do bloqueio de saudação **myLock**.

tipo Hello fornecido é o tipo de recurso de toohello específico. Para o armazenamento, defina Olá tipo too"Microsoft.Storage/storageaccounts/providers/locks".

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Bloquear implantado recursos com o Azure PowerShell usando Olá [AzureRmResourceLock novo](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.

toolock um recurso, forneça o nome de saudação do recurso de saudação, seu tipo de recurso e o nome do grupo de recursos.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

tooget informações sobre um bloqueio, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget todos os bloqueios de saudação em sua assinatura, use:

```powershell
Get-AzureRmResourceLock
```

tooget todos os bloqueios de um recurso, use:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget todos os bloqueios para um grupo de recursos, use:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

PowerShell do Azure oferece outros comandos para bloqueios de trabalho, tais como [conjunto AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate um bloqueio e [AzureRmResourceLock remover](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete um bloqueio.

## <a name="azure-cli"></a>CLI do Azure

Bloquear implantado recursos com CLI do Azure usando Olá [bloqueio az criar](/cli/azure/lock#create) comando.

toolock um recurso, forneça o nome de saudação do recurso de saudação, seu tipo de recurso e o nome do grupo de recursos.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

tooget informações sobre um bloqueio, use [lista de bloqueio az](/cli/azure/lock#list). tooget todos os bloqueios de saudação em sua assinatura, use:

```azurecli
az lock list
```

tooget todos os bloqueios de um recurso, use:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget todos os bloqueios para um grupo de recursos, use:

```azurecli
az lock list --resource-group exampleresourcegroup
```

CLI do Azure oferece outros comandos para bloqueios de trabalho, tais como [atualização de bloqueio az](/cli/azure/lock#update) tooupdate um bloqueio e [bloqueio az excluir](/cli/azure/lock#delete) toodelete um bloqueio.

## <a name="rest-api"></a>API REST
Você pode bloquear recursos implantados com hello [API REST para bloqueios de gerenciamento](https://docs.microsoft.com/rest/api/resources/managementlocks). Olá REST API permite toocreate e excluir bloqueios e recuperar informações sobre bloqueios existentes.

toocreate um bloqueio, execute:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso. Olá nome do bloqueio é tudo o que você quiser toocall bloqueio de saudação. Para a api-version, use **2015-01-01**.

Na solicitação de hello, inclua um objeto JSON que especifica propriedades Olá para bloqueio de saudação.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Próximas etapas
* Para saber mais sobre como trabalhar com bloqueios de recursos, confira [Bloquear os recursos do Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn sobre logicamente organizar seus recursos, consulte [usando marcas tooorganize seus recursos](resource-group-using-tags.md)
* toochange reside de um recurso com a qual grupo de recursos, consulte [Mover grupo de recursos de toonew de recursos](resource-group-move-resources.md)
* É possível aplicar restrições e convenções em sua assinatura com políticas personalizadas. Para obter mais informações, consulte [recursos de toomanage de política de uso e controlar o acesso](resource-manager-policy.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

