---
title: "Como marcar uma máquina virtual Linux do Azure | Microsoft Docs"
description: "Saiba como marcar uma máquina virtual Linux do Azure criada no Azure usando o modelo de implantação do Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="1cf60-103">Como marcar uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="1cf60-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="1cf60-104">Este artigo descreve as diferentes maneiras de marcar uma máquina virtual do Linux no Azure por meio do modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1cf60-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="1cf60-105">As marcas são pares de chave/valor definidos pelo usuário que podem ser colocados diretamente em um recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1cf60-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="1cf60-106">Atualmente, o Azure oferece suporte a até 15 marcas por recurso e grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1cf60-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="1cf60-107">As marcas podem ser colocadas em um recurso no momento da criação ou adicionadas a um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="1cf60-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="1cf60-108">Observe que as marcas tem suporte apenas para recursos criados por meio do modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1cf60-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="1cf60-109">Marcando com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1cf60-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="1cf60-110">Para começar, é necessário ter a última [CLI do Azure 2.0 (Visualização)](/cli/azure/install-az-cli2) instalada e conectada a uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1cf60-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1cf60-111">Você também pode executar essas etapas com a [CLI 1.0 do Azure](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cf60-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1cf60-112">É possível exibir todas as propriedades de uma determinada Máquina Virtual, incluindo as marcas, usando este comando:</span><span class="sxs-lookup"><span data-stu-id="1cf60-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="1cf60-113">Para adicionar uma nova marcação de VM usando a CLI do Azure, use o comando `azure vm update`, juntamente com o parâmetro de marcação **--set**:</span><span class="sxs-lookup"><span data-stu-id="1cf60-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="1cf60-114">Para remover as marcas, use o parâmetro **--remove** no comando `azure vm update`.</span><span class="sxs-lookup"><span data-stu-id="1cf60-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="1cf60-115">Agora que aplicamos marcas aos nossos recursos por meio do CLI do Azure e do Portal, vamos examinar os detalhes de uso para ver as marcas no portal de cobrança.</span><span class="sxs-lookup"><span data-stu-id="1cf60-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="1cf60-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1cf60-116">Next steps</span></span>
* <span data-ttu-id="1cf60-117">Para saber mais sobre como marcar seus recursos do Azure, consulte [Visão geral do Azure Resource Manager][Azure Resource Manager Overview] e [Usando marcas para organizar os Recursos do Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="1cf60-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="1cf60-118">Para ver como as marcas podem ajudá-lo a gerenciar seu uso de recursos do Azure, consulte [Noções básicas de sua fatura do Azure][Understanding your Azure Bill] e [Obtenha informações sobre o consumo de recursos do Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="1cf60-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
