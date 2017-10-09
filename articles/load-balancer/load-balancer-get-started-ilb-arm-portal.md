---
title: aaaCreate um balanceador de carga interno - portal do Azure | Microsoft Docs
description: "Saiba como toocreate um interno balanceador de carga no Resource Manager usando Olá portal do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="079c2-103">Criar um balanceador de carga interno no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="079c2-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="079c2-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="079c2-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="079c2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="079c2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="079c2-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="079c2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="079c2-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="079c2-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="079c2-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="079c2-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="079c2-109">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="079c2-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="079c2-110">Introdução à criação de um balanceador de carga interno usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="079c2-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="079c2-111">Use Olá seguir etapas toocreate um balanceador de carga interno de saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="079c2-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="079c2-112">Abra um navegador, navegue toohello [portal do Azure](http://portal.azure.com)e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="079c2-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="079c2-113">No hello superior esquerda da tela hello, clique em **novo** > **rede** > **balanceador de carga**.</span><span class="sxs-lookup"><span data-stu-id="079c2-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="079c2-114">Em Olá **criar balanceador de carga** folha, insira um **nome** para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="079c2-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="079c2-115">Em **Esquema**, clique em **Interno**.</span><span class="sxs-lookup"><span data-stu-id="079c2-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="079c2-116">Clique em **rede Virtual**, e, em seguida, selecione Olá onde você deseja que o balanceador de carga Olá toocreate de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="079c2-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="079c2-117">Se você não vir a rede virtual hello, você deseja toouse, verifique Olá **local** você está usando para o balanceador de carga hello e alterá-lo adequadamente.</span><span class="sxs-lookup"><span data-stu-id="079c2-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="079c2-118">Clique em **sub-rede**e selecione a sub-rede Olá onde você deseja que o balanceador de carga toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="079c2-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="079c2-119">Em **atribuição de endereço IP**, clique em **dinâmico** ou **estático**, dependendo se você quiser Olá endereço IP para Olá carga toobe da balanceador fixo (estático) ou não.</span><span class="sxs-lookup"><span data-stu-id="079c2-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="079c2-120">Se você selecionar toouse um endereço IP estático, você terá tooprovide um endereço Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="079c2-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="079c2-121">Em **grupo de recursos** especifique nome de Olá de um novo grupo de recursos para o balanceador de carga hello, ou clique em **selecionar existentes** e selecione um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="079c2-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="079c2-122">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="079c2-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="079c2-123">Configuração de regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="079c2-123">Configure load balancing rules</span></span>

<span data-ttu-id="079c2-124">Após Olá criação de Balanceador de carga, navegue até tooconfigure de recurso de Balanceador de carga toohello-lo.</span><span class="sxs-lookup"><span data-stu-id="079c2-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="079c2-125">Você precisará tooconfigure primeiro um pool de endereços de back-end e uma investigação antes de configurar uma regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="079c2-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="079c2-126">Etapa 1: Configurar um pool de back-end</span><span class="sxs-lookup"><span data-stu-id="079c2-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="079c2-127">No portal do Azure de Olá, clique em **procurar** > **balanceadores de carga**e, em seguida, clique em balanceador de carga Olá criado acima.</span><span class="sxs-lookup"><span data-stu-id="079c2-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="079c2-128">Em Olá **configurações** folha, clique em **pools de back-end**.</span><span class="sxs-lookup"><span data-stu-id="079c2-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="079c2-129">Em Olá **pools de endereços de back-end** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="079c2-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="079c2-130">Em Olá **Adicionar pool de back-end** folha, insira um **nome** para pool de back-end hello e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="079c2-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="079c2-131">Etapa 2: Configurar uma investigação</span><span class="sxs-lookup"><span data-stu-id="079c2-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="079c2-132">No portal do Azure de Olá, clique em **procurar** > **balanceadores de carga**e, em seguida, clique em balanceador de carga Olá criado acima.</span><span class="sxs-lookup"><span data-stu-id="079c2-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="079c2-133">Em Olá **configurações** folha, clique em **testes**.</span><span class="sxs-lookup"><span data-stu-id="079c2-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="079c2-134">Em Olá **testes** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="079c2-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="079c2-135">Em Olá **adicionar teste** folha, insira um **nome** para investigação hello.</span><span class="sxs-lookup"><span data-stu-id="079c2-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="079c2-136">Em **Protocolo**, selecione **HTTP** (para os sites da Web) ou **TCP** (para outros aplicativos baseados no TCP).</span><span class="sxs-lookup"><span data-stu-id="079c2-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="079c2-137">Em **porta**, especifique Olá porta toouse ao acessar a investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="079c2-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="079c2-138">Em **caminho** (para HTTP testes somente), especifique Olá caminho toouse como um teste.</span><span class="sxs-lookup"><span data-stu-id="079c2-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="079c2-139">Em **intervalo** especificar com que frequência tooprobe Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="079c2-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="079c2-140">Em **limite não íntegro**, especifique o número de tentativas devem falhar antes Olá máquina de virtual de back-end está marcada como não íntegra.</span><span class="sxs-lookup"><span data-stu-id="079c2-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="079c2-141">Clique em **Okey** toocreate investigação.</span><span class="sxs-lookup"><span data-stu-id="079c2-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="079c2-142">Etapa 3: Configurar regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="079c2-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="079c2-143">No portal do Azure de Olá, clique em **procurar** > **balanceadores de carga**e, em seguida, clique em balanceador de carga Olá criado acima.</span><span class="sxs-lookup"><span data-stu-id="079c2-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="079c2-144">Em Olá **configurações** folha, clique em **regras de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="079c2-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="079c2-145">Em Olá **regras de balanceamento de carga** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="079c2-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="079c2-146">Em Olá **regra de balanceamento de carga de adicionar** folha, insira um **nome** para regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="079c2-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="079c2-147">Em **Protocolo**, selecione **HTTP** (para os sites da Web) ou **TCP** (para outros aplicativos baseados no TCP).</span><span class="sxs-lookup"><span data-stu-id="079c2-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="079c2-148">Em **porta**, especificar tooin balanceador de carga de saudação de conexão de clientes de porta de saudação.</span><span class="sxs-lookup"><span data-stu-id="079c2-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="079c2-149">Em **porta de back-end**, especifique Olá porta toobe usado no pool de back-end de saudação (geralmente, porta do balanceador de carga hello e a porta de back-end de saudação são Olá mesmo).</span><span class="sxs-lookup"><span data-stu-id="079c2-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="079c2-150">Em **pool de back-end**, selecione Olá back-end pool que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="079c2-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="079c2-151">Em **persistência de sessão**, selecione como você deseja toopersist sessões.</span><span class="sxs-lookup"><span data-stu-id="079c2-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="079c2-152">Em **tempo limite de ociosidade (minutos)**, especifique o tempo limite de ociosidade hello.</span><span class="sxs-lookup"><span data-stu-id="079c2-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="079c2-153">Em **IP flutuante (retorno de servidor direto)**, clique em **Desabilitado** ou **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="079c2-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="079c2-154">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="079c2-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="079c2-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="079c2-155">Next steps</span></span>

[<span data-ttu-id="079c2-156">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="079c2-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="079c2-157">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="079c2-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

