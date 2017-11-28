---
title: Criar um balanceador de carga interno - Portal do Azure | Microsoft Docs
description: Saiba como criar um balanceador de carga interno no Resource Manager usando o portal do Azure
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
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="6d5fc-103">Criar um Balanceador de carga interno no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d5fc-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d5fc-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d5fc-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="6d5fc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d5fc-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="6d5fc-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6d5fc-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="6d5fc-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="6d5fc-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="6d5fc-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fc-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6d5fc-109">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fc-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="6d5fc-110">Introdução à criação de um balanceador de carga interno usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d5fc-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="6d5fc-111">Use as etapas a seguir para criar um balanceador de carga interno no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="6d5fc-112">Abra um navegador, navegue até o [portal do Azure](http://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="6d5fc-113">No canto superior esquerdo da tela, clique em **Novo** > **Rede** > **Balanceador de carga**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="6d5fc-114">Na folha **Criar balanceador de carga**, insira um **Nome** para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="6d5fc-115">Em **Esquema**, clique em **Interno**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="6d5fc-116">Clique em **Rede virtual**e selecione a rede virtual na qual você deseja criar o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d5fc-117">Caso você não veja a rede virtual que deseja usar, verifique o **Local** que você está usando para o balanceador de carga e altere-o adequadamente.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-117">If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="6d5fc-118">Clique em **Sub-rede**e selecione a sub-rede onde você quer criar o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="6d5fc-119">Em **Atribuição do endereço IP**, clique em **Dinâmico** ou **Estático**, dependendo de você querer que o endereço IP para o balanceador de carga seja fixo (estático) ou não.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d5fc-120">Se você optar por usar um endereço IP estático, será necessário fornecer um endereço para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-120">If you select to use a static IP address, you will have to provide an address for the load balancer.</span></span>

8. <span data-ttu-id="6d5fc-121">Em **Grupo de recursos**, especifique o nome de um novo grupo de recursos para o balanceador de carga ou clique em **selecionar existente** e selecione um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="6d5fc-122">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="6d5fc-123">Configuração de regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="6d5fc-123">Configure load balancing rules</span></span>

<span data-ttu-id="6d5fc-124">Após a criação do balanceador de carga, navegue até o recurso do balanceador de carga para configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="6d5fc-125">Primeiro, você precisa configurar um pool de endereços back-end e uma investigação antes de configurar uma regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="6d5fc-126">Etapa 1: Configurar um pool de back-end</span><span class="sxs-lookup"><span data-stu-id="6d5fc-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="6d5fc-127">No portal do Azure, clique em **Procurar** > **Balanceadores de carga**, em seguida, clique no balanceador de carga que você criou acima.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="6d5fc-128">Na folha **Configurações**, clique nos **Pools de back-end**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="6d5fc-129">Na folha **Pools de endereços de back-end**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="6d5fc-130">Na folha **Adicionar pool de back-end**, insira um **Nome** para o pool de back-end e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="6d5fc-131">Etapa 2: Configurar uma investigação</span><span class="sxs-lookup"><span data-stu-id="6d5fc-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="6d5fc-132">No portal do Azure, clique em **Procurar** > **Balanceadores de carga**, em seguida, clique no balanceador de carga que você criou acima.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="6d5fc-133">Na folha **Configurações**, clique em **Investigações**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="6d5fc-134">Na folha **Investigações**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="6d5fc-135">Na folha **Adicionar investigação**, insira um **Nome** para a investigação.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="6d5fc-136">Em **Protocolo**, selecione **HTTP** (para os sites da Web) ou **TCP** (para outros aplicativos baseados no TCP).</span><span class="sxs-lookup"><span data-stu-id="6d5fc-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="6d5fc-137">Em **Porta**, especifique a porta a ser usada ao acessar a investigação.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="6d5fc-138">Em **Caminho** (apenas para investigações HTTP), especifique o caminho a ser usado como uma investigação.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="6d5fc-139">Em **Intervalo** , especifique a frequência de investigação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="6d5fc-140">Em **Limite não íntegro**, especifique quantas tentativas devem falhar antes que a máquina virtual de back-end seja marcada como não íntegra.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="6d5fc-141">Clique em **OK** para criar a investigação.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="6d5fc-142">Etapa 3: Configurar regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="6d5fc-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="6d5fc-143">No portal do Azure, clique em **Procurar** > **Balanceadores de carga**, em seguida, clique no balanceador de carga que você criou acima.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="6d5fc-144">Na folha **Configurações**, clique em **Regras de balanceamento da carga**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="6d5fc-145">Na folha **Regras de balanceamento da carga**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="6d5fc-146">Na folha **Adicionar regra balanceamento da carga**, insira um **Nome** para a regra.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="6d5fc-147">Em **Protocolo**, selecione **HTTP** (para os sites da Web) ou **TCP** (para outros aplicativos baseados no TCP).</span><span class="sxs-lookup"><span data-stu-id="6d5fc-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="6d5fc-148">Em **Porta**, especifique a porta que os clientes conectam no balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="6d5fc-149">Em **Porta back-end**, especifique a porta a ser usada no pool de back-end (normalmente, a porta do balanceador de carga e a porta de back-end são iguais).</span><span class="sxs-lookup"><span data-stu-id="6d5fc-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="6d5fc-150">Em **Pool de back-end**, selecione o pool de back-end criado acima.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="6d5fc-151">Em **Persistência da sessão**, selecione como você deseja que as sessões persistam.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="6d5fc-152">Em **Tempo limite de ociosidade (minutos)**, especifique o tempo limite de ociosidade.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="6d5fc-153">Em **IP flutuante (retorno de servidor direto)**, clique em **Desabilitado** ou **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="6d5fc-154">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d5fc-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d5fc-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d5fc-155">Next steps</span></span>

[<span data-ttu-id="6d5fc-156">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="6d5fc-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="6d5fc-157">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="6d5fc-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

