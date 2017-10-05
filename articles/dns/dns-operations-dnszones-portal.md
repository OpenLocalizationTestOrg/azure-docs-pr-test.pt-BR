---
title: "Gerenciar as zonas DNS no DNS do Azure – Portal do Azure | Microsoft Docs"
description: "Você pode gerenciar zonas DNS usando o Portal do Azure. Este artigo descreve como atualizar, excluir e criar zonas DNS no DNS do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="7d5e5-104">Como gerenciar zonas DNS usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7d5e5-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d5e5-105">Portal</span><span class="sxs-lookup"><span data-stu-id="7d5e5-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="7d5e5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d5e5-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="7d5e5-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7d5e5-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="7d5e5-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7d5e5-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="7d5e5-109">Este artigo mostra como gerenciar suas zonas DNS usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="7d5e5-110">Você também pode gerenciar as zonas DNS usando a plataforma cruzada [CLI do Azure](dns-operations-dnszones-cli.md) ou o Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="7d5e5-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="7d5e5-111">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d5e5-111">Create a DNS zone</span></span>

1. <span data-ttu-id="7d5e5-112">Entrar no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7d5e5-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="7d5e5-113">No menu Hub, clique em **Novo > Rede >**, em seguida, clique em **Zona DNS** para abrir a folha Criar zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="7d5e5-115">Na folha **Criar zona DNS**, insira os seguintes valores e clique em **Criar**:</span><span class="sxs-lookup"><span data-stu-id="7d5e5-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="7d5e5-116">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-116">**Setting**</span></span> | <span data-ttu-id="7d5e5-117">**Valor**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-117">**Value**</span></span> | <span data-ttu-id="7d5e5-118">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7d5e5-119">**Nome**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-119">**Name**</span></span>|<span data-ttu-id="7d5e5-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="7d5e5-120">contoso.com</span></span>|<span data-ttu-id="7d5e5-121">O nome da zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d5e5-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="7d5e5-122">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-122">**Subscription**</span></span>|<span data-ttu-id="7d5e5-123">[Sua assinatura]</span><span class="sxs-lookup"><span data-stu-id="7d5e5-123">[Your subscription]</span></span>|<span data-ttu-id="7d5e5-124">Selecione uma assinatura para criar a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="7d5e5-125">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-125">**Resource group**</span></span>|<span data-ttu-id="7d5e5-126">**Criar um novo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="7d5e5-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="7d5e5-127">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-127">Create a resource group.</span></span> <span data-ttu-id="7d5e5-128">O nome do grupo de recursos deve ser exclusivo na assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="7d5e5-129">Para saber mais sobre grupos de recursos, leia o artigo [Visão geral do Gerenciador de Recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="7d5e5-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7d5e5-130">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="7d5e5-130">**Location**</span></span>|<span data-ttu-id="7d5e5-131">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="7d5e5-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="7d5e5-132">O grupo de recursos se refere ao local do grupo de recursos e não tem impacto sobre o local da zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="7d5e5-133">O local da zona DNS sempre é "global" e não é exibido.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="7d5e5-134">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="7d5e5-134">List DNS zones</span></span>

<span data-ttu-id="7d5e5-135">No Portal do Azure, navegue até **Mais serviços** > **Rede** > **Zonas DNS**.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="7d5e5-136">Cada zona DNS é seu próprio recurso, informações como o número de conjuntos de registro e servidores de nomes são visíveis nesse modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="7d5e5-137">A coluna **SERVIDORES DE NOMES** não está no modo de exibição padrão. Para adicioná-la, clique em **Colunas**, selecione **Servidores de nomes** e clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![listagem de zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="7d5e5-139">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d5e5-139">Delete a DNS zone</span></span>

<span data-ttu-id="7d5e5-140">Navegue até uma zona DNS no portal.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="7d5e5-141">Na folha **Zona DNS**, clique em **Excluir zona**.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="7d5e5-142">Você deverá confirmar que deseja excluir a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="7d5e5-143">Excluir uma zona DNS também exclui todos os registros que estão contidos na zona.</span><span class="sxs-lookup"><span data-stu-id="7d5e5-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d5e5-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d5e5-144">Next steps</span></span>

<span data-ttu-id="7d5e5-145">Aprenda a trabalhar com sua zona DNS e registros visitando [Introdução ao DNS do Azure usando o Portal do Azure](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7d5e5-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>