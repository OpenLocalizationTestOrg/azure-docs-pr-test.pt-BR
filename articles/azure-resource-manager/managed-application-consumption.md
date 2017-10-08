---
title: aplicativo gerenciado de aaaConsume do Azure | Microsoft Docs
description: Descreve como um cliente cria um aplicativo gerenciado do Azure a partir dos arquivos publicados.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Consumir um aplicativo gerenciado interno

Consuma [aplicativos gerenciados](managed-application-overview.md) do Azure destinados aos membros de sua organização. Por exemplo, selecione os aplicativos gerenciados de seu departamento de TI que garantem a conformidade com os padrões organizacionais. Esses aplicativos gerenciados estão disponíveis por meio de saudação catálogo de serviços, hello Azure Marketplace.

Antes de continuar com este artigo, você deve ter um aplicativo gerenciado disponível no catálogo de serviços Olá para sua assinatura. Se alguém em sua organização ainda não tiver criado um aplicativo gerenciado, consulte [Publicar um aplicativo gerenciado para consumo interno](managed-application-publishing.md).

No momento, você pode usar a CLI do Azure ou Olá tooconsume portal do Azure um aplicativo gerenciado.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Criar o aplicativo hello gerenciado usando o portal de saudação

toodeploy um aplicativo gerenciado por meio do portal hello, siga estas etapas:

1. Vá toohello portal do Azure. Pesquise **Aplicativo Gerenciado do Catálogo de Serviços**.

   ![Aplicativo gerenciado do Catálogo de Serviços](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Selecione Olá gerenciados aplicativo deseja toocreate da lista de saudação das soluções disponíveis. Selecione **Criar**.

   ![Seleção do aplicativo gerenciado](./media/managed-application-consumption/select-offer.png)

1. Forneça valores para parâmetros de saudação que são necessárias tooprovision Olá recursos. Selecione **Centro-Oeste dos EUA** para local. Selecione **OK**.

   ![Parâmetros do aplicativo gerenciado](./media/managed-application-consumption/input-parameters.png)

1. modelo de saudação valida valores hello fornecidos. Se a validação for bem-sucedida, selecione **Okey** toostart implantação de saudação.

   ![Validação de aplicativo gerenciado](./media/managed-application-consumption/validation.png)

Após a conclusão da implantação hello, os recursos adequados Olá definidos no modelo de saudação são provisionados no grupo de recurso gerenciado Olá fornecida.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Criar um aplicativo hello gerenciado usando a CLI do Azure

Há dois toocreate de maneiras um aplicativo gerenciado usando a CLI do Azure:

* Use o comando Olá para criação de aplicativos gerenciados.
* Use o comando de implantação de modelo regular hello.

### <a name="use-hello-template-deployment-command"></a>Use o comando de implantação de modelo Olá

Implante arquivo applianceMainTemplate.json Olá Olá fornecedor criado.

Depois crie dois grupos de recursos. Olá primeiro grupo de recursos é onde hello recursos de aplicativo gerenciado é criado: Microsoft.Solutions/appliances. segundo grupo de recursos Olá contém todos os recursos de saudação definidos em mainTemplate.json. Este grupo de recursos é gerenciado pelo Olá ISV.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Use `westcentralus` como local de Olá Olá do grupo de recursos.
>

toodeploy applianceMainTemplate.json em mainResourceGroup, use Olá comando a seguir:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Após Olá anterior é executado de modelo, ele solicitará Olá valores de parâmetros de saudação que são definidos no modelo de saudação. Além disso toohello parâmetros que são necessários tooprovision recursos em um modelo, você precisa de dois valores de parâmetro de chave:

- **managedResourceGroupId**: Olá ID da saudação recurso grupo contentor Olá recursos definidos no applianceMainTemplate.json. Olá ID tem o formato de saudação `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. Em Olá anterior de exemplo, ele do ID de saudação do `managedResourceGroup`.
- **applianceDefinitionId**: ID de saudação do hello gerenciados recursos de definição de aplicativo. Esse valor é fornecido pelo Olá ISV.

> [!NOTE]
> publicador Olá deve conceder o grupo de recursos do acesso toohello que contém a definição do aplicativo hello gerenciado. recursos de definição de saudação é criado na assinatura do publicador hello. Portanto, um usuário, grupo de usuário ou aplicativo no locatário de saudação do cliente precisa de acesso de leitura toothis recurso.

Depois de implantação Olá concluída com êxito, você verá Olá gerenciado aplicativo é criado no mainResourceGroup. recurso de storageAccount de saudação é criado no managedResourceGroup.

### <a name="use-hello-create-command"></a>Saudação de uso criar comando

Você pode usar o hello `az managedapp create` comando toocreate um aplicativo gerenciado de saudação gerenciado a definição do aplicativo.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **ferramenta de definição de Id**: ID de recurso de saudação do hello gerenciado criada no hello anterior da etapa de definição de aplicativo. tooobtain essa ID, executar Olá comando a seguir:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Esse comando retorna a definição de aplicativo hello gerenciado. Você precisa de valor de saudação da propriedade de ID de saudação.

* **gerenciado-rg-id**: nome de saudação do hello recurso grupo contentor Olá recursos definidos no applianceMainTemplate.json. Esse recurso é grupo de recurso gerenciado hello. Ele é gerenciado pelo editor de saudação. Se não existir, ele será criado para você.
* **grupo de recursos**: grupo de recursos de saudação onde Olá gerenciada recursos de aplicativo é criado. Olá Microsoft.Solutions/appliance recurso reside no grupo de recursos.
* **parâmetros**: Olá parâmetros que são necessários para os recursos de saudação definidos em applianceMainTemplate.json.

## <a name="known-issues"></a>Problemas conhecidos

Esta versão de preview inclui Olá problemas a seguir:

* Um erro de servidor interno 500 é exibido durante a criação de saudação do aplicativo hello gerenciado. Se você encontrar esse problema, é provável toobe intermitente. Repita a operação de saudação.
* Um novo grupo de recursos é necessária para o grupo de recurso gerenciado hello. Se você usar um grupo de recursos existente, a implantação de saudação falhará.
* Olá grupo de recursos que contém o recurso de Microsoft.Solutions/appliances Olá deve ser criado no hello **westcentralus** local.

## <a name="next-steps"></a>Próximas etapas

* Para aplicativos de toomanaged uma introdução, consulte [visão geral do aplicativo gerenciado](managed-application-overview.md).
* Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).
* Para obter informações sobre publicação toohello de aplicativos gerenciados do Azure Marketplace, consulte [Azure gerenciados aplicativos Olá Marketplace](managed-application-author-marketplace.md).
* Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).
