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
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="2d7ef-103">Use marcas tooorganize seus recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2d7ef-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="2d7ef-104">Você pode aplicar marcas tooresources única que oferece suporte a operações do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="2d7ef-105">Se você criou uma máquina virtual, a rede virtual ou a conta de armazenamento por meio do modelo de implantação clássico hello (por exemplo, como por meio Olá portal clássico do Azure), você não pode aplicar um recurso de toothat de marca.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="2d7ef-106">toosupport marcação, reimplante esses recursos por meio do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="2d7ef-107">Todos os outros recursos oferecem suporte à marcação.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="2d7ef-108">Políticas para consistência de marca</span><span class="sxs-lookup"><span data-stu-id="2d7ef-108">Policies for tag consistency</span></span>

<span data-ttu-id="2d7ef-109">Você pode usar regras de toocreate de diretivas de recursos padrão para sua organização.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="2d7ef-110">Você pode criar políticas que certifique-se de que recursos estão marcados com valores apropriados hello.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="2d7ef-111">Para obter mais informações, consulte [Aplicar políticas de recursos para marcas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="2d7ef-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d7ef-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="2d7ef-113">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2d7ef-113">Azure CLI</span></span>

<span data-ttu-id="2d7ef-114">toosee Olá marcas existentes para um *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="2d7ef-115">Esse script retorna Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="2d7ef-116">toosee Olá marcas existentes para um *recurso que tem uma ID de recurso especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="2d7ef-117">Ou, toosee Olá marcas existentes para um *recurso que tem um grupo específico de nome, o tipo e o recurso*, use:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="2d7ef-118">grupos de recursos tooget que têm uma marca específica, use `az group list`:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="2d7ef-119">tooget todos os recursos de saudação que têm uma marca específica e um valor, use `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="2d7ef-120">Quando você aplica marcas tooa recurso ou um grupo de recursos, você pode substituir as marcas existentes Olá nesse recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="2d7ef-121">Portanto, você deve usar uma abordagem diferente com base em se o recurso de saudação ou grupo de recursos tem marcas existentes.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="2d7ef-122">tooadd marcas tooa *grupo de recursos sem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="2d7ef-123">tooadd marcas tooa *recurso sem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="2d7ef-124">tooadd marcas tooa de recurso que já tem marcas, recuperar marcas existentes hello, reformatar esse valor e reaplicar as marcas existentes e novas hello:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="2d7ef-125">tooapply todas as marcas de recursos do tooits um grupo de recursos, e *não reter marcas existentes nos recursos de saudação*, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

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

<span data-ttu-id="2d7ef-126">tooapply todas as marcas de recursos do tooits um grupo de recursos, e *reter marcas existentes nos recursos*, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d7ef-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="2d7ef-127">Modelos</span><span class="sxs-lookup"><span data-stu-id="2d7ef-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="2d7ef-128">Portal</span><span class="sxs-lookup"><span data-stu-id="2d7ef-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="2d7ef-129">API REST</span><span class="sxs-lookup"><span data-stu-id="2d7ef-129">REST API</span></span>
<span data-ttu-id="2d7ef-130">Olá portal do Azure e o PowerShell usam Olá [REST API do Gerenciador de recursos](https://docs.microsoft.com/rest/api/resources/) em segundo plano da saudação.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="2d7ef-131">Se você precisar toointegrate marcação em outro ambiente, você pode obter marcas usando **obter** Olá recurso ID e atualização Olá conjunto de marcas usando um **PATCH** chamar.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="2d7ef-132">Marcas e cobrança</span><span class="sxs-lookup"><span data-stu-id="2d7ef-132">Tags and billing</span></span>
<span data-ttu-id="2d7ef-133">Você pode usar marcas toogroup seus dados de cobrança.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="2d7ef-134">Por exemplo, se você estiver executando várias VMs para organizações diferentes, use Olá marcas toogroup uso pelo Centro de custo.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="2d7ef-135">Você também pode usar marcas toocategorize custos pelo ambiente de tempo de execução, como o uso de cobrança Olá para VMs em execução no ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="2d7ef-136">Você pode recuperar informações sobre marcas por meio de saudação [uso de recursos do Azure e APIs RateCard](../billing/billing-usage-rate-card-overview.md) ou arquivo de valores separados por vírgulas (CSV) de uso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="2d7ef-137">Baixar o arquivo de uso de saudação do hello [portal de conta do Azure](https://account.windowsazure.com/) ou [portal EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="2d7ef-138">Para obter mais informações sobre toobilling acesso programático, consulte [obter ideias sobre o consumo de recursos do Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="2d7ef-139">Para operações de API REST, confira [Referência da API REST de cobrança do Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="2d7ef-140">Quando você baixar uso Olá CSV para serviços que oferecem suporte a marcas de cobrança, marcas de saudação aparecem no hello **marcas** coluna.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="2d7ef-141">Para saber mais, confira [Entenda sua fatura do Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Ver as marcas de cobranças](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="2d7ef-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d7ef-143">Next steps</span></span>
* <span data-ttu-id="2d7ef-144">É possível aplicar restrições e convenções em sua assinatura usando políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="2d7ef-145">Uma política que você definir pode exigir que todos os recursos tenham uma valor para uma marcação específica.</span><span class="sxs-lookup"><span data-stu-id="2d7ef-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="2d7ef-146">Para obter mais informações, consulte [usar políticas toomanage recursos e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="2d7ef-147">Para uma introdução toousing PowerShell do Azure quando você estiver implantando recursos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="2d7ef-148">Para uma saudação de toousing Introdução CLI do Azure quando você estiver implantando recursos, consulte [hello usando a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="2d7ef-149">Para o portal de saudação do toousing uma introdução, consulte [usando os recursos do Azure de toomanage portal do Azure Olá](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="2d7ef-150">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2d7ef-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

