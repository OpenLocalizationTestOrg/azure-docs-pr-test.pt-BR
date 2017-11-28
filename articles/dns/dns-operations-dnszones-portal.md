---
title: aaaManage DNS zonas no DNS do Azure - portal do Azure | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando Olá portal do Azure. Este artigo descreve como tooupdate, excluir e criar zonas DNS no DNS do Azure"
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="cc00f-104">Como zonas DNS toomanage Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cc00f-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc00f-105">Portal</span><span class="sxs-lookup"><span data-stu-id="cc00f-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="cc00f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc00f-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="cc00f-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="cc00f-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="cc00f-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="cc00f-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="cc00f-109">Este artigo mostra como toomanage suas zonas DNS usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc00f-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="cc00f-110">Você também pode gerenciar as zonas DNS usando multiplataforma Olá [CLI do Azure](dns-operations-dnszones-cli.md) ou hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="cc00f-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="cc00f-111">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="cc00f-111">Create a DNS zone</span></span>

1. <span data-ttu-id="cc00f-112">Entrar toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cc00f-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="cc00f-113">No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="cc00f-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="cc00f-115">Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="cc00f-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="cc00f-116">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="cc00f-116">**Setting**</span></span> | <span data-ttu-id="cc00f-117">**Valor**</span><span class="sxs-lookup"><span data-stu-id="cc00f-117">**Value**</span></span> | <span data-ttu-id="cc00f-118">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="cc00f-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="cc00f-119">**Nome**</span><span class="sxs-lookup"><span data-stu-id="cc00f-119">**Name**</span></span>|<span data-ttu-id="cc00f-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="cc00f-120">contoso.com</span></span>|<span data-ttu-id="cc00f-121">nome de saudação da zona do DNS de saudação</span><span class="sxs-lookup"><span data-stu-id="cc00f-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="cc00f-122">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="cc00f-122">**Subscription**</span></span>|<span data-ttu-id="cc00f-123">[Sua assinatura]</span><span class="sxs-lookup"><span data-stu-id="cc00f-123">[Your subscription]</span></span>|<span data-ttu-id="cc00f-124">Selecione uma zona DNS assinatura toocreate Olá no.</span><span class="sxs-lookup"><span data-stu-id="cc00f-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="cc00f-125">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="cc00f-125">**Resource group**</span></span>|<span data-ttu-id="cc00f-126">**Criar um novo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="cc00f-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="cc00f-127">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc00f-127">Create a resource group.</span></span> <span data-ttu-id="cc00f-128">nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="cc00f-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="cc00f-129">toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.</span><span class="sxs-lookup"><span data-stu-id="cc00f-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="cc00f-130">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="cc00f-130">**Location**</span></span>|<span data-ttu-id="cc00f-131">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cc00f-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="cc00f-132">grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc00f-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="cc00f-133">local da zona DNS Olá sempre é "global" e não é mostrado.</span><span class="sxs-lookup"><span data-stu-id="cc00f-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="cc00f-134">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="cc00f-134">List DNS zones</span></span>

<span data-ttu-id="cc00f-135">Olá portal do Azure no, navegue muito**mais serviços** > **rede** > **zonas DNS**.</span><span class="sxs-lookup"><span data-stu-id="cc00f-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="cc00f-136">Cada zona DNS é seu próprio recurso, informações como o número de conjuntos de registro e servidores de nomes são visíveis nesse modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="cc00f-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="cc00f-137">coluna Olá **servidores de nome** não está no modo de exibição de padrão de saudação, tooadd ele clique **colunas**, selecione **servidores de nome** e clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="cc00f-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![listagem de zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="cc00f-139">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="cc00f-139">Delete a DNS zone</span></span>

<span data-ttu-id="cc00f-140">Navegue tooa zona DNS no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc00f-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="cc00f-141">Em Olá **zona DNS** folha, clique em **Excluir zona**.</span><span class="sxs-lookup"><span data-stu-id="cc00f-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="cc00f-142">Você está tooconfirm solicitado são desejarem zona DNS toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="cc00f-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="cc00f-143">Também excluir uma zona DNS exclui todos os registros de saudação que estão contidos na zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc00f-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc00f-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc00f-144">Next steps</span></span>

<span data-ttu-id="cc00f-145">Saiba como toowork com a zona DNS e registros visitando [Introdução ao DNS do Azure usando o portal do Azure de saudação](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cc00f-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
