---
title: "aaaHow tootag um recurso de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Saiba mais sobre a marcação de uma máquina virtual do Windows criada no Azure usando o modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="f2b0c-103">Como tootag uma máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="f2b0c-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="f2b0c-104">Este artigo descreve as diferentes maneiras tootag uma máquina virtual do Windows no Azure por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f2b0c-105">As marcas são pares de chave/valor definidos pelo usuário que podem ser colocados diretamente em um recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="f2b0c-106">Azure atualmente oferece suporte a marcas de too15 por grupo de recursos e recursos.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="f2b0c-107">Marcas podem ser colocadas em um recurso no tempo de saudação da criação ou adicionado o recurso existente tooan.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="f2b0c-108">Observe que as marcas são suportadas para recursos criados por meio do modelo de implantação de Gerenciador de recursos de saudação apenas.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="f2b0c-109">Se você quiser tootag uma máquina virtual Linux, consulte [como tootag uma máquina virtual do Linux no Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2b0c-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="f2b0c-110">Marcação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2b0c-110">Tagging with PowerShell</span></span>
<span data-ttu-id="f2b0c-111">toocreate, adicionar e excluir marcas por meio do PowerShell, é necessário primeiro tooset o seu [ambiente do PowerShell do Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="f2b0c-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="f2b0c-112">Depois de concluir a instalação hello, você pode colocar marcas de recursos de computação, rede e armazenamento no momento da criação ou após Olá recurso for criado por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="f2b0c-113">Este artigo se concentra na exibição/edição de marcas colocadas nas Máquinas Virtuais.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="f2b0c-114">Navega pela primeira vez, tooa Máquina Virtual por meio de saudação `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="f2b0c-115">Se sua máquina Virtual já contém marcas, você verá todas as marcas de saudação no recurso:</span><span class="sxs-lookup"><span data-stu-id="f2b0c-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="f2b0c-116">Se você desejar marcas tooadd por meio do PowerShell, você pode usar o hello `Set-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="f2b0c-117">Observe que, ao atualizar marcas pelo PowerShell, as marcas são atualizadas como um todo.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="f2b0c-118">Portanto, se você estiver adicionando um recurso de tooa de marca que já tem marcas, será necessário tooinclude todas as marcas de saudação que você deseja toobe colocado no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="f2b0c-119">Abaixo está um exemplo de como tooadd adicional marcas tooa recursos por meio de Cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="f2b0c-120">Esse cmdlet primeiro define todas Olá marcas colocadas em *MyTestVM* toohello *$tags* variável, usando Olá `Get-AzureRmResource` e `Tags` propriedade.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="f2b0c-121">Olá segundo comando exibe marcas Olá para Olá dado variável.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-121">hello second command displays hello tags for hello given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="f2b0c-122">Olá terceiro comando adiciona uma marca adicionais toohello *$tags* variável.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="f2b0c-123">Observe o uso de saudação do hello  **+=**  tooappend Olá toohello de par chave/valor novo *$tags* lista.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="f2b0c-124">comando quarto Olá define todas as marcas de saudação definidas na saudação de *$tags* toohello variável considerando os recursos.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="f2b0c-125">Nesse caso, é MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="f2b0c-126">Olá quinto comando exibe todas as marcas de saudação no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="f2b0c-127">Como você pode ver, *local* agora está definido como uma marca com *MyLocation* como valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2b0c-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="f2b0c-128">Saiba mais sobre toolearn marcação por meio do PowerShell, check-out Olá [Cmdlets de recursos do Azure][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="f2b0c-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="f2b0c-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2b0c-129">Next steps</span></span>
* <span data-ttu-id="f2b0c-130">toolearn mais informações sobre a marcação de recursos do Azure, consulte [visão geral do Gerenciador de recursos do Azure] [ Azure Resource Manager Overview] e [tooorganize marcas usando os recursos do Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="f2b0c-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="f2b0c-131">toosee como marcas podem ajudá-lo a gerenciar o uso de recursos do Azure, consulte [Noções básicas sobre sua conta do Azure] [ Understanding your Azure Bill] e [obter ideias sobre o consumo de recursos do Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="f2b0c-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
