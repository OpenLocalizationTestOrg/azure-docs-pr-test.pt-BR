---
title: "aaaTag Azure recursos para organização lógica | Microsoft Docs"
description: "Mostra como tooapply marcas tooorganize Azure recursos para cobrança e gerenciamento."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Use marcas tooorganize seus recursos do Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Você pode aplicar marcas tooresources única que oferece suporte a operações do Gerenciador de recursos do Azure. Se você criou uma máquina virtual, a rede virtual ou a conta de armazenamento por meio do modelo de implantação clássico hello (por exemplo, como por meio Olá portal clássico do Azure), você não pode aplicar um recurso de toothat de marca. toosupport marcação, reimplante esses recursos por meio do Gerenciador de recursos. Todos os outros recursos oferecem suporte à marcação.
> 
> 

## <a name="policies-for-tag-consistency"></a>Políticas para consistência de marca

Você pode usar regras de toocreate de diretivas de recursos padrão para sua organização. Você pode criar políticas que certifique-se de que recursos estão marcados com valores apropriados hello. Para obter mais informações, consulte [Aplicar políticas de recursos para marcas](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>CLI do Azure

toosee Olá marcas existentes para um *grupo de recursos*, use:

```azurecli
az group show -n examplegroup --query tags
```

Esse script retorna Olá formato a seguir:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee Olá marcas existentes para um *recurso que tem uma ID de recurso especificado*, use:

```azurecli
az resource show --id {resource-id} --query tags
```

Ou, toosee Olá marcas existentes para um *recurso que tem um grupo específico de nome, o tipo e o recurso*, use:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

grupos de recursos tooget que têm uma marca específica, use `az group list`:

```azurecli
az group list --tag Dept=IT
```

tooget todos os recursos de saudação que têm uma marca específica e um valor, use `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Quando você aplica marcas tooa recurso ou um grupo de recursos, você pode substituir as marcas existentes Olá nesse recurso ou grupo de recursos. Portanto, você deve usar uma abordagem diferente com base em se o recurso de saudação ou grupo de recursos tem marcas existentes. 

tooadd marcas tooa *grupo de recursos sem marcas existentes*, use:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd marcas tooa *recurso sem marcas existentes*, use:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd marcas tooa de recurso que já tem marcas, recuperar marcas existentes hello, reformatar esse valor e reaplicar as marcas existentes e novas hello: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply todas as marcas de recursos do tooits um grupo de recursos, e *não reter marcas existentes nos recursos de saudação*, use Olá script a seguir:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

tooapply todas as marcas de recursos do tooits um grupo de recursos, e *reter marcas existentes nos recursos*, use Olá script a seguir:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>Modelos

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>API REST
Olá portal do Azure e o PowerShell usam Olá [REST API do Gerenciador de recursos](https://docs.microsoft.com/rest/api/resources/) em segundo plano da saudação. Se você precisar toointegrate marcação em outro ambiente, você pode obter marcas usando **obter** Olá recurso ID e atualização Olá conjunto de marcas usando um **PATCH** chamar.

## <a name="tags-and-billing"></a>Marcas e cobrança
Você pode usar marcas toogroup seus dados de cobrança. Por exemplo, se você estiver executando várias VMs para organizações diferentes, use Olá marcas toogroup uso pelo Centro de custo. Você também pode usar marcas toocategorize custos pelo ambiente de tempo de execução, como o uso de cobrança Olá para VMs em execução no ambiente de produção de hello.


Você pode recuperar informações sobre marcas por meio de saudação [uso de recursos do Azure e APIs RateCard](../billing/billing-usage-rate-card-overview.md) ou arquivo de valores separados por vírgulas (CSV) de uso de saudação. Baixar o arquivo de uso de saudação do hello [portal de conta do Azure](https://account.windowsazure.com/) ou [portal EA](https://ea.azure.com). Para obter mais informações sobre toobilling acesso programático, consulte [obter ideias sobre o consumo de recursos do Microsoft Azure](../billing/billing-usage-rate-card-overview.md). Para operações de API REST, confira [Referência da API REST de cobrança do Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Quando você baixar uso Olá CSV para serviços que oferecem suporte a marcas de cobrança, marcas de saudação aparecem no hello **marcas** coluna. Para saber mais, confira [Entenda sua fatura do Microsoft Azure](../billing/billing-understand-your-bill.md).

![Ver as marcas de cobranças](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Próximas etapas
* É possível aplicar restrições e convenções em sua assinatura usando políticas personalizadas. Uma política que você definir pode exigir que todos os recursos tenham uma valor para uma marcação específica. Para obter mais informações, consulte [usar políticas toomanage recursos e controlar o acesso](resource-manager-policy.md).
* Para uma introdução toousing PowerShell do Azure quando você estiver implantando recursos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](powershell-azure-resource-manager.md).
* Para uma saudação de toousing Introdução CLI do Azure quando você estiver implantando recursos, consulte [hello usando a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).
* Para o portal de saudação do toousing uma introdução, consulte [usando os recursos do Azure de toomanage portal do Azure Olá](resource-group-portal.md).  
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

