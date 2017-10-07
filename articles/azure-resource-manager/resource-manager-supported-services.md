---
title: aaaAzure provedores de recursos e tipos de recurso | Microsoft Docs
description: "Descreve os provedores de recursos Olá que dão suporte ao Gerenciador de recursos, esquemas e as versões de API disponíveis e regiões de saudação que podem hospedar recursos hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Provedores e tipos de recursos

Ao implantar os recursos, você precisa frequentemente tooretrieve informações sobre provedores de recursos hello e tipos. Neste artigo, você aprende a:

* Exibir todos os provedores de recursos no Azure
* Verificar o status do registro de um provedor de recursos
* Registrar um provedor de recursos
* Exibir os tipos de recurso para um provedor de recursos
* Exibir localizações válidas para um tipo de recurso
* Exibir versões de API válidas para um tipo de recurso

Você pode executar essas etapas através do portal hello, PowerShell ou CLI do Azure.

## <a name="powershell"></a>PowerShell

toosee todos os provedores de recursos no Azure e o status de registro Olá para sua assinatura, usam:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Que retorna resultados semelhantes a:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Registrando um provedor de recursos configura toowork sua assinatura com o provedor de recursos de saudação. escopo de saudação para o registro é sempre assinatura hello. Por padrão, muitos provedores de recursos são automaticamente registrados. No entanto, talvez seja necessário toomanually registrar alguns provedores de recursos. tooregister um provedor de recursos, você deve ter a saudação de tooperform permissão `/register/action` operação para o provedor de recursos hello. Esta operação está incluída no hello Colaborador e funções de proprietário.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Que retorna resultados semelhantes a:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.

informações de toosee para um provedor de recursos específico, use:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Que retorna resultados semelhantes a:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

tipos de recurso de saudação toosee para um provedor de recursos, use:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Que retorna:

```powershell
batchAccounts
operations
locations
locations/quotas
```

versão da API Olá corresponde versão tooa de operações da API REST que são lançadas pelo provedor de recursos de saudação. Como um provedor de recursos permite que os novos recursos, ele lança uma nova versão de hello API REST. 

tooget Olá API versões disponíveis para um tipo de recurso, use:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Que retorna:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Gerenciador de recursos tem suporte em todas as regiões, mas os recursos de saudação que implantar talvez não tenha suporte em todas as regiões. Além disso, pode haver limitações que impedem o uso de algumas regiões que dão suporte ao recurso de saudação em sua assinatura. 

use tooget locais de saudação com suporte para um tipo de recurso.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Que retorna:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>CLI do Azure
toosee todos os provedores de recursos no Azure e o status de registro Olá para sua assinatura, usam:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Que retorna resultados semelhantes a:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Registrando um provedor de recursos configura toowork sua assinatura com o provedor de recursos de saudação. escopo de saudação para o registro é sempre assinatura hello. Por padrão, muitos provedores de recursos são automaticamente registrados. No entanto, talvez seja necessário toomanually registrar alguns provedores de recursos. tooregister um provedor de recursos, você deve ter a saudação de tooperform permissão `/register/action` operação para o provedor de recursos hello. Esta operação está incluída no hello Colaborador e funções de proprietário.

```azurecli
az provider register --namespace Microsoft.Batch
```

Que retorna uma mensagem de que o registro está em andamento.

Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.

informações de toosee para um provedor de recursos específico, use:

```azurecli
az provider show --namespace Microsoft.Batch
```

Que retorna resultados semelhantes a:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

tipos de recurso de saudação toosee para um provedor de recursos, use:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Que retorna:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

versão da API Olá corresponde versão tooa de operações da API REST que são lançadas pelo provedor de recursos de saudação. Como um provedor de recursos permite que os novos recursos, ele lança uma nova versão de hello API REST. 

tooget Olá API versões disponíveis para um tipo de recurso, use:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Que retorna:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Gerenciador de recursos tem suporte em todas as regiões, mas os recursos de saudação que implantar talvez não tenha suporte em todas as regiões. Além disso, pode haver limitações que impedem o uso de algumas regiões que dão suporte ao recurso de saudação em sua assinatura. 

use tooget locais de saudação com suporte para um tipo de recurso.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Que retorna:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Portal

toosee todos os provedores de recursos no Azure e o status de registro Olá para sua assinatura, selecione **assinaturas**.

![selecionar assinaturas](./media/resource-manager-supported-services/select-subscriptions.png)

Escolha Olá tooview de assinatura.

![especificar a assinatura](./media/resource-manager-supported-services/subscription.png)

Selecione **provedores de recursos** e exiba a lista de saudação de provedores de recursos disponíveis.

![mostrar provedores de recursos](./media/resource-manager-supported-services/show-resource-providers.png)

Registrando um provedor de recursos configura toowork sua assinatura com o provedor de recursos de saudação. escopo de saudação para o registro é sempre assinatura hello. Por padrão, muitos provedores de recursos são automaticamente registrados. No entanto, talvez seja necessário toomanually registrar alguns provedores de recursos. tooregister um provedor de recursos, você deve ter a saudação de tooperform permissão `/register/action` operação para o provedor de recursos hello. Esta operação está incluída no hello Colaborador e funções de proprietário. tooregister um provedor de recursos, selecione **registrar**.

![registrar provedor de recursos](./media/resource-manager-supported-services/register-provider.png)

Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.

informações de toosee para um provedor de recurso específico, selecione **mais serviços**.

![selecionar mais serviços](./media/resource-manager-supported-services/more-services.png)

Procurar **Gerenciador de recursos** e selecioná-lo entre as opções disponíveis de saudação.

![selecionar resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

Selecione **Provedores**.

![Selecionar provedores](./media/resource-manager-supported-services/select-providers.png)

Recursos e o provedor de recursos Olá selecione tipo que você deseja tooview.

![Selecionar tipo de recurso](./media/resource-manager-supported-services/select-resource-type.png)

Gerenciador de recursos tem suporte em todas as regiões, mas os recursos de saudação que implantar talvez não tenha suporte em todas as regiões. Além disso, pode haver limitações que impedem o uso de algumas regiões que dão suporte ao recurso de saudação em sua assinatura. Gerenciador de recursos de saudação exibe locais válidos para o tipo de recurso hello.

![Mostrar localizações](./media/resource-manager-supported-services/show-locations.png)

versão da API Olá corresponde versão tooa de operações da API REST que são lançadas pelo provedor de recursos de saudação. Como um provedor de recursos permite que os novos recursos, ele lança uma nova versão de hello API REST. Gerenciador de recursos de saudação exibe as versões de API válidas para o tipo de recurso hello.

![Mostrar versões de API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como criar modelos do Gerenciador de recursos, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sobre a implantação de recursos, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).
* operações de saudação tooview para um provedor de recursos, consulte [API REST do Azure](/rest/api/).

