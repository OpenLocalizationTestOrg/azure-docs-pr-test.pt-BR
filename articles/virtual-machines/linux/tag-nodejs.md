---
title: "aaaHow tootag uma máquina virtual de Linux do Azure | Microsoft Docs"
description: "Saiba mais sobre a marcação de uma máquina virtual do Azure Linux criada no Azure usando o modelo de implantação do Gerenciador de recursos de saudação."
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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="679e5-103">Como tootag uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="679e5-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="679e5-104">Este artigo descreve as diferentes maneiras tootag uma máquina de virtual do Linux no Azure por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="679e5-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="679e5-105">As marcas são pares de chave/valor definidos pelo usuário que podem ser colocados diretamente em um recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="679e5-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="679e5-106">Azure atualmente oferece suporte a marcas de too15 por grupo de recursos e recursos.</span><span class="sxs-lookup"><span data-stu-id="679e5-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="679e5-107">Marcas podem ser colocadas em um recurso no tempo de saudação da criação ou adicionado o recurso existente tooan.</span><span class="sxs-lookup"><span data-stu-id="679e5-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="679e5-108">Observe que as marcas que têm suporte para recursos criados por meio do modelo de implantação de Gerenciador de recursos de saudação apenas.</span><span class="sxs-lookup"><span data-stu-id="679e5-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="679e5-109">Marcando com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="679e5-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="679e5-110">toobegin, [instalar e configurar Olá CLI do Azure](../../xplat-cli-azure-resource-manager.md) e verifique se você está no modo do Gerenciador de recursos (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="679e5-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="679e5-111">Você pode exibir todas as propriedades para uma determinada máquina Virtual, incluindo marcas hello, usando este comando:</span><span class="sxs-lookup"><span data-stu-id="679e5-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="679e5-112">tooadd uma nova marca VM por meio de saudação CLI do Azure, você pode usar o hello `azure vm set` comando junto com o parâmetro de marca hello **-t**:</span><span class="sxs-lookup"><span data-stu-id="679e5-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="679e5-113">tooremove todas as marcas, você pode usar o hello **– T** parâmetro hello `azure vm set` comando.</span><span class="sxs-lookup"><span data-stu-id="679e5-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="679e5-114">Agora que estamos aplicou marcas tooour recursos CLI do Azure e Olá Portal, vamos dar uma olhada em toosee de detalhes de uso de saudação marcas Olá no portal de cobrança hello.</span><span class="sxs-lookup"><span data-stu-id="679e5-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="679e5-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="679e5-115">Next steps</span></span>
* <span data-ttu-id="679e5-116">toolearn mais informações sobre a marcação de recursos do Azure, consulte [visão geral do Gerenciador de recursos do Azure] [ Azure Resource Manager Overview] e [tooorganize marcas usando os recursos do Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="679e5-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="679e5-117">toosee como marcas podem ajudá-lo a gerenciar o uso de recursos do Azure, consulte [Noções básicas sobre sua conta do Azure] [ Understanding your Azure Bill] e [obter ideias sobre o consumo de recursos do Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="679e5-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
