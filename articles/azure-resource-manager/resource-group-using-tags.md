---
title: "Marcar recursos do Azure para organização lógica | Microsoft Docs"
description: "Mostra como aplicar marcas para organizar os recursos do Azure para cobrança e gerenciamento."
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
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="b8a53-103">Usar marcações para organizar seus recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="b8a53-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="b8a53-104">Você pode aplicar marcas apenas a recursos que oferecem suporte a operações do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8a53-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="b8a53-105">Se você tiver criado uma máquina virtual, uma rede virtual ou uma conta de armazenamento por meio do modelo de implantação clássica (como o portal clássico do Azure), não poderá aplicar uma marca a esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b8a53-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="b8a53-106">Para dar suporte à marcação, implante esses recursos novamente por meio do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8a53-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="b8a53-107">Todos os outros recursos oferecem suporte à marcação.</span><span class="sxs-lookup"><span data-stu-id="b8a53-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="b8a53-108">Políticas para consistência de marca</span><span class="sxs-lookup"><span data-stu-id="b8a53-108">Policies for tag consistency</span></span>

<span data-ttu-id="b8a53-109">Você pode usar políticas de recursos para criar regras padrão para sua organização.</span><span class="sxs-lookup"><span data-stu-id="b8a53-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="b8a53-110">Você pode criar políticas que garantem que os recursos sejam marcados com os valores apropriados.</span><span class="sxs-lookup"><span data-stu-id="b8a53-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="b8a53-111">Para obter mais informações, consulte [Aplicar políticas de recursos para marcas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="b8a53-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8a53-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="b8a53-113">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b8a53-113">Azure CLI</span></span>

<span data-ttu-id="b8a53-114">Para conferir as marcas existentes para um *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="b8a53-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="b8a53-115">Esse script retorna o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="b8a53-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="b8a53-116">Para conferir as marcas existentes para um *recurso que tem uma ID de recurso especificada*, use:</span><span class="sxs-lookup"><span data-stu-id="b8a53-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="b8a53-117">Ou, para conferir as marcas existentes para um *recurso que tem um nome, tipo e um grupo de recursos especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="b8a53-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="b8a53-118">Para obter grupos de recursos que têm uma marca específica, use `az group list`:</span><span class="sxs-lookup"><span data-stu-id="b8a53-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="b8a53-119">Para obter todos os recursos que tem marca e valor específicos, use `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="b8a53-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="b8a53-120">Ao aplicar marcas a um recurso ou grupo de recursos, você pode substituir as marcas existentes nesse recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8a53-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="b8a53-121">Portanto, você deve usar uma abordagem diferente com base em se o recurso ou o grupo de recursos tem marcas existentes.</span><span class="sxs-lookup"><span data-stu-id="b8a53-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="b8a53-122">Para adicionar marcas a um *grupo de recursos sem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="b8a53-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="b8a53-123">Para adicionar marcas a um *recurso sem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="b8a53-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="b8a53-124">Para adicionar marcas a um recurso que já tem marcas, recupere as marcas existentes, reformate esse valor e reaplique as marcas novas e existentes:</span><span class="sxs-lookup"><span data-stu-id="b8a53-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="b8a53-125">Para aplicar todas as marcas de um grupo de recursos em seus recursos, e *não manter as marcas existentes nos recursos*, use o seguinte script:</span><span class="sxs-lookup"><span data-stu-id="b8a53-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

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

<span data-ttu-id="b8a53-126">Para aplicar todas as marcações de um grupo de recursos a seus recursos e *reter as marcações existentes nos recursos*, use o seguinte script:</span><span class="sxs-lookup"><span data-stu-id="b8a53-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="b8a53-127">Modelos</span><span class="sxs-lookup"><span data-stu-id="b8a53-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="b8a53-128">Portal</span><span class="sxs-lookup"><span data-stu-id="b8a53-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="b8a53-129">API REST</span><span class="sxs-lookup"><span data-stu-id="b8a53-129">REST API</span></span>
<span data-ttu-id="b8a53-130">O portal do Azure e o PowerShell usam a [API REST do Gerenciador de Recursos](https://docs.microsoft.com/rest/api/resources/) em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b8a53-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="b8a53-131">Se você precisar integrar a marcação a outro ambiente, você pode obter marcas usando **GET** na ID do recurso e atualizar o conjunto de marcas usando uma chamada de **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="b8a53-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="b8a53-132">Marcas e cobrança</span><span class="sxs-lookup"><span data-stu-id="b8a53-132">Tags and billing</span></span>
<span data-ttu-id="b8a53-133">Você pode usar marcas para agrupar os dados de cobrança.</span><span class="sxs-lookup"><span data-stu-id="b8a53-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="b8a53-134">Por exemplo, se você estiver executando várias VMs para organizações diferentes, use as marcas para a utilização do grupo por centro de custo.</span><span class="sxs-lookup"><span data-stu-id="b8a53-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="b8a53-135">Você também pode usar marcas para categorizar os custos pelo ambiente de tempo de execução, como por exemplo, o uso de cobrança para VMs em execução no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b8a53-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="b8a53-136">Você pode recuperar as informações sobre as marcações por meio das [APIs RateCard e Uso de Recursos do Azure](../billing/billing-usage-rate-card-overview.md) ou do arquivo de uso CSV (com valores separados por vírgula).</span><span class="sxs-lookup"><span data-stu-id="b8a53-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="b8a53-137">Baixe o arquivo de uso no [portal de contas do Azure](https://account.windowsazure.com/) ou no [portal de EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8a53-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="b8a53-138">Para saber mais sobre o acesso programático às informações de cobrança, confira [Obter informações sobre o consumo de recursos do Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="b8a53-139">Para operações de API REST, confira [Referência da API REST de cobrança do Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="b8a53-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="b8a53-140">Quando você baixa o CSV de uso para serviços que dão suporte a marcações com cobrança, as marcações aparecerão na coluna **Marcações** .</span><span class="sxs-lookup"><span data-stu-id="b8a53-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="b8a53-141">Para saber mais, confira [Entenda sua fatura do Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Ver as marcas de cobranças](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="b8a53-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8a53-143">Next steps</span></span>
* <span data-ttu-id="b8a53-144">É possível aplicar restrições e convenções em sua assinatura usando políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b8a53-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="b8a53-145">Uma política que você definir pode exigir que todos os recursos tenham uma valor para uma marcação específica.</span><span class="sxs-lookup"><span data-stu-id="b8a53-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="b8a53-146">Para saber mais, confira [Usar políticas para gerenciar recursos e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="b8a53-147">Para obter uma introdução ao uso do Azure PowerShell ao implantar recursos, confira [Usando o Azure PowerShell com o Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b8a53-148">Para obter uma introdução ao uso da CLI do Azure ao implantar recursos, confira [Usando a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b8a53-149">Para obter uma introdução ao uso do portal, confira [Usando o portal do Azure para gerenciar os recursos do Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="b8a53-150">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b8a53-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

