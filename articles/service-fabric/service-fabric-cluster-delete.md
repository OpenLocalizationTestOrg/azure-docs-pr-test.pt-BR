---
title: aaaDelete um Azure cluster e seus recursos | Microsoft Docs
description: "Saiba como delete toocompletely uma malha de serviço de cluster ou excluir grupo de recursos de saudação contendo cluster hello ou excluindo seletivamente recursos."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="23b71-103">Excluir um cluster do Service Fabric nos recursos do Azure e hello usa</span><span class="sxs-lookup"><span data-stu-id="23b71-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="23b71-104">Um cluster do Service Fabric é composto por muitos outros recursos do Azure além de recurso de cluster toohello propriamente dito.</span><span class="sxs-lookup"><span data-stu-id="23b71-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="23b71-105">Para toocompletely exclua um cluster do Service Fabric também é necessário toodelete que todos Olá recursos que é formado.</span><span class="sxs-lookup"><span data-stu-id="23b71-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="23b71-106">Você tem duas opções: grupo de recursos ou excluir Olá Olá cluster está em (que exclui o recurso de cluster hello e todos os outros recursos no grupo de recursos de saudação) ou excluir especificamente o recurso de cluster de saudação e associado recursos (mas não outras recursos no grupo de recursos de saudação).</span><span class="sxs-lookup"><span data-stu-id="23b71-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="23b71-107">Excluindo o recurso de cluster Olá **não** excluir todos os Olá outros recursos que o cluster do Service Fabric é composto de.</span><span class="sxs-lookup"><span data-stu-id="23b71-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="23b71-108">Excluir grupo de recursos inteiro da saudação (RG) que Olá malha do serviço de cluster está em</span><span class="sxs-lookup"><span data-stu-id="23b71-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="23b71-109">Isso é Olá tooensure de maneira mais fácil que você exclua todos os recursos de saudação associados ao cluster, incluindo o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23b71-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="23b71-110">Você pode excluir o grupo de recursos de saudação usando o PowerShell ou por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23b71-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="23b71-111">Se seu grupo de recursos tiver recursos que não estão relacionadas tooService cluster de malha, você pode excluir recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="23b71-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="23b71-112">Excluir grupo de recursos de saudação usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="23b71-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="23b71-113">Você também pode excluir o grupo de recursos de saudação executando Olá seguintes cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="23b71-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="23b71-114">Certifique-se de que o Azure PowerShell 1.0 ou superior está instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="23b71-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="23b71-115">Se você não tiver feito isso antes, execute as etapas de saudação descritas em [como tooinstall e configurar o Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="23b71-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="23b71-116">Abra uma janela do PowerShell e execute Olá PS cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="23b71-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="23b71-117">Você obterá uma exclusão de saudação do prompt tooconfirm se você não usou Olá *-Force* opção.</span><span class="sxs-lookup"><span data-stu-id="23b71-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="23b71-118">Em confirmação Olá RG e todos os recursos de saudação que ele contém são excluídos.</span><span class="sxs-lookup"><span data-stu-id="23b71-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="23b71-119">Excluir um grupo de recursos em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23b71-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="23b71-120">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23b71-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="23b71-121">Navegue cluster do Service Fabric toohello toodelete desejado.</span><span class="sxs-lookup"><span data-stu-id="23b71-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="23b71-122">Clique em Olá nome do grupo de recursos na página do essentials cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23b71-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="23b71-123">Isso traz Olá **princípios básicos de grupo de recursos** página.</span><span class="sxs-lookup"><span data-stu-id="23b71-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="23b71-124">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="23b71-124">Click **Delete**.</span></span>
6. <span data-ttu-id="23b71-125">Siga as instruções de saudação em que página toocomplete Olá a exclusão do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23b71-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Exclusão do Grupo de Recursos][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="23b71-127">Excluir o recurso de cluster hello e Olá recursos usados por ele, mas não outros recursos no grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="23b71-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="23b71-128">Se seu grupo de recursos tem apenas os recursos relacionados toohello malha do serviço de cluster deseja toodelete, ele é mais fácil toodelete Olá todo recurso grupo.</span><span class="sxs-lookup"><span data-stu-id="23b71-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="23b71-129">Se você desejar que recursos de saudação do tooselectively excluir um por um no seu grupo de recursos, em seguida, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="23b71-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="23b71-130">Se você implantou o cluster usando o portal de saudação ou usando um dos modelos de serviço Gerenciador de recursos de malha Olá Olá da Galeria de modelos, todos os recursos de Olá Olá cluster usará são marcados com hello duas marcas a seguir.</span><span class="sxs-lookup"><span data-stu-id="23b71-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="23b71-131">Você pode usar toodecide quais recursos você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="23b71-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="23b71-132">***Marca n º 1:*** chave = clusterName, valor = 'nome do cluster de saudação'</span><span class="sxs-lookup"><span data-stu-id="23b71-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="23b71-133">***Marcação n º 2:*** Chave = resourceName, Valor = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="23b71-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="23b71-134">Excluir recursos específicos no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23b71-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="23b71-135">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23b71-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="23b71-136">Navegue cluster do Service Fabric toohello toodelete desejado.</span><span class="sxs-lookup"><span data-stu-id="23b71-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="23b71-137">Vá muito**todas as configurações de** na folha do essentials hello.</span><span class="sxs-lookup"><span data-stu-id="23b71-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="23b71-138">Clique em **marcas** em **gerenciamento de recursos** na folha de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="23b71-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="23b71-139">Clique em uma saudação **marcas** em Olá marcas folha tooget uma lista de todos os recursos de saudação com essa marca.</span><span class="sxs-lookup"><span data-stu-id="23b71-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Marcações de recursos][ResourceTags]
6. <span data-ttu-id="23b71-141">Uma vez que a lista de saudação de recursos marcados, clique em cada um dos recursos de saudação e excluí-los.</span><span class="sxs-lookup"><span data-stu-id="23b71-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Recursos marcados][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="23b71-143">Excluir recursos hello usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="23b71-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="23b71-144">Você pode excluir recursos Olá um por um executando Olá seguintes cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="23b71-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="23b71-145">Certifique-se de que o Azure PowerShell 1.0 ou superior está instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="23b71-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="23b71-146">Se você não tiver feito isso antes, execute as etapas de saudação descritas em [como tooinstall e configurar o Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="23b71-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="23b71-147">Abra uma janela do PowerShell e execute Olá PS cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="23b71-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="23b71-148">Para cada um dos recursos de saudação você deseja toodelete, execute o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="23b71-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="23b71-149">recurso de cluster em Olá toodelete, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="23b71-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="23b71-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23b71-150">Next steps</span></span>
<span data-ttu-id="23b71-151">Saudação de leitura após tooalso Saiba mais sobre particionamento serviços e atualizar um cluster:</span><span class="sxs-lookup"><span data-stu-id="23b71-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="23b71-152">Saiba mais sobre atualizações de cluster</span><span class="sxs-lookup"><span data-stu-id="23b71-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="23b71-153">Saiba mais sobre os serviços com estado de particionamento para escala máxima</span><span class="sxs-lookup"><span data-stu-id="23b71-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
