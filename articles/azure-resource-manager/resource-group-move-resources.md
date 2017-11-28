---
title: aaaMove recursos do Azure toonew assinatura ou grupo de recursos | Microsoft Docs
description: Use o Gerenciador de recursos do Azure toomove recursos tooa novo grupo de recursos ou assinatura.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="6006e-103">Mover grupo de recursos toonew de recursos ou assinatura</span><span class="sxs-lookup"><span data-stu-id="6006e-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="6006e-104">Este tópico mostra como toomove recursos tooeither uma nova assinatura ou um novo recurso de grupo no hello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="6006e-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="6006e-105">Você pode usar o portal hello, o PowerShell, CLI do Azure ou Olá recursos de toomove da API REST.</span><span class="sxs-lookup"><span data-stu-id="6006e-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="6006e-106">operações de movimentação de saudação neste tópico são tooyou disponível sem qualquer assistência do suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="6006e-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="6006e-107">Ao mover recursos, grupo de saudação de origem e o grupo de destino Olá são bloqueadas durante a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="6006e-108">Gravar e operações de exclusão estão bloqueados em grupos de recursos de saudação até que seja concluída Olá move.</span><span class="sxs-lookup"><span data-stu-id="6006e-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="6006e-109">Esse bloqueio significa que você não pode adicionar, atualizar ou excluir recursos em grupos de recursos de saudação, mas isso não significa que recursos Olá congelados.</span><span class="sxs-lookup"><span data-stu-id="6006e-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="6006e-110">Por exemplo, se você mover um SQL Server e seu banco de dados tooa novo grupo de recursos, um aplicativo que usa o banco de dados de saudação experiências sem tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="6006e-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="6006e-111">Ele pode ler e gravar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6006e-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="6006e-112">Você não pode alterar o local de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="6006e-113">Mover um recurso só move tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="6006e-114">Olá novo grupo de recursos pode ter um local diferente, mas que não altera a localização de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="6006e-115">Este artigo descreve como a conta ofertas toomove recursos dentro do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="6006e-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="6006e-116">Se você realmente quiser toochange sua conta do Azure, oferecendo (como atualizar do pagamento de toopre pré-pago) enquanto continua toowork com recursos existentes, consulte [alternar sua oferta de assinatura do Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="6006e-117">Lista de verificação antes de mover recursos</span><span class="sxs-lookup"><span data-stu-id="6006e-117">Checklist before moving resources</span></span>
<span data-ttu-id="6006e-118">Há algumas etapas importantes tooperform antes de mover um recurso.</span><span class="sxs-lookup"><span data-stu-id="6006e-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="6006e-119">Ao verificar essas condições, é possível evitar erros.</span><span class="sxs-lookup"><span data-stu-id="6006e-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="6006e-120">Olá assinaturas de origem e de destino devem existir no hello mesmo [locatário do Active Directory do Azure](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="6006e-121">toocheck ambas as assinaturas têm Olá mesmo ID de locatário, use o Azure PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6006e-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="6006e-122">Para o Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="6006e-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="6006e-123">Para a CLI 2.0 do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="6006e-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="6006e-124">Se Olá locatário IDs para assinaturas de origem e destino Olá não são Olá mesmo, você pode tentar toochange diretório de saudação para assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="6006e-125">No entanto, essa opção está apenas disponível tooService administradores que está conectado com uma conta da Microsoft (não uma conta organizacional).</span><span class="sxs-lookup"><span data-stu-id="6006e-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="6006e-126">alterando o diretório hello, login toohello de tooattempt [portal clássico](https://manage.windowsazure.com/)e selecione **configurações**e selecione a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="6006e-127">Se hello **Editar diretório** ícone estiver disponível, selecione-a como toochange Olá associado do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6006e-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![editar diretório](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="6006e-129">Se esse ícone não estiver disponível, você deve entrar em contato com o suporte toomove Olá recursos tooa novo locatário.</span><span class="sxs-lookup"><span data-stu-id="6006e-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="6006e-130">serviço de saudação deve habilitar recursos de toomove de capacidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="6006e-131">Este tópico lista quais serviços permitem mover os recursos e quais serviços não habilitam a movimentação dos recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="6006e-132">assinatura de destino Olá deve ser registrada para provedor de recursos de saudação do recurso hello está sendo movido.</span><span class="sxs-lookup"><span data-stu-id="6006e-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="6006e-133">Se não, você recebe um erro informando que Olá **assinatura não está registrada para um tipo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="6006e-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="6006e-134">Você pode encontrar esse problema ao mover uma nova assinatura de recursos tooa, mas essa assinatura nunca foi usada com o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="6006e-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="6006e-135">toolearn como toocheck Olá status de registro e registrar provedores de recursos, consulte [provedores de recursos e tipos de](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="6006e-136">Quando o suporte toocall</span><span class="sxs-lookup"><span data-stu-id="6006e-136">When toocall support</span></span>
<span data-ttu-id="6006e-137">Você pode mover a maioria dos recursos por meio de operações de autoatendimento Olá mostradas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="6006e-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="6006e-138">Use operações de autoatendimento Olá para:</span><span class="sxs-lookup"><span data-stu-id="6006e-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="6006e-139">Mova os recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6006e-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="6006e-140">Mover recursos clássicos de acordo com o toohello [limitações de implantação clássico](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="6006e-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="6006e-141">Telefonar para o suporte quando você precisa:</span><span class="sxs-lookup"><span data-stu-id="6006e-141">Call support when you need to:</span></span>

* <span data-ttu-id="6006e-142">Mova recursos tooa nova conta do Azure (e locatário do Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="6006e-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="6006e-143">Mover recursos clássicos, mas está tendo problemas com as limitações de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="6006e-144">Serviços que permitem mover</span><span class="sxs-lookup"><span data-stu-id="6006e-144">Services that enable move</span></span>
<span data-ttu-id="6006e-145">Por enquanto, serviços de saudação que permitem que um novo grupo de recursos de movimentação tooboth e assinatura são:</span><span class="sxs-lookup"><span data-stu-id="6006e-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="6006e-146">Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="6006e-146">API Management</span></span>
* <span data-ttu-id="6006e-147">Aplicativos do Serviço de Aplicativo (aplicativos Web) - consulte [Limitações do Serviço de Aplicativo](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="6006e-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="6006e-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="6006e-148">Application Insights</span></span>
* <span data-ttu-id="6006e-149">Automação</span><span class="sxs-lookup"><span data-stu-id="6006e-149">Automation</span></span>
* <span data-ttu-id="6006e-150">Batch</span><span class="sxs-lookup"><span data-stu-id="6006e-150">Batch</span></span>
* <span data-ttu-id="6006e-151">Bing Mapas</span><span class="sxs-lookup"><span data-stu-id="6006e-151">Bing Maps</span></span>
* <span data-ttu-id="6006e-152">CDN</span><span class="sxs-lookup"><span data-stu-id="6006e-152">CDN</span></span>
* <span data-ttu-id="6006e-153">Serviços de Nuvem - veja [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="6006e-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="6006e-154">Serviços Cognitivos</span><span class="sxs-lookup"><span data-stu-id="6006e-154">Cognitive Services</span></span>
* <span data-ttu-id="6006e-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="6006e-155">Content Moderator</span></span>
* <span data-ttu-id="6006e-156">Catálogo de Dados</span><span class="sxs-lookup"><span data-stu-id="6006e-156">Data Catalog</span></span>
* <span data-ttu-id="6006e-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="6006e-157">Data Factory</span></span>
* <span data-ttu-id="6006e-158">Análises Data Lake</span><span class="sxs-lookup"><span data-stu-id="6006e-158">Data Lake Analytics</span></span>
* <span data-ttu-id="6006e-159">Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="6006e-159">Data Lake Store</span></span>
* <span data-ttu-id="6006e-160">DNS</span><span class="sxs-lookup"><span data-stu-id="6006e-160">DNS</span></span>
* <span data-ttu-id="6006e-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6006e-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="6006e-162">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="6006e-162">Event Hubs</span></span>
* <span data-ttu-id="6006e-163">Clusters HDInsight – veja [Limitações do HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="6006e-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="6006e-164">Hubs IoT</span><span class="sxs-lookup"><span data-stu-id="6006e-164">IoT Hubs</span></span>
* <span data-ttu-id="6006e-165">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="6006e-165">Key Vault</span></span>
* <span data-ttu-id="6006e-166">Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="6006e-166">Load Balancers</span></span>
* <span data-ttu-id="6006e-167">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="6006e-167">Logic Apps</span></span>
* <span data-ttu-id="6006e-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6006e-168">Machine Learning</span></span>
* <span data-ttu-id="6006e-169">Serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="6006e-169">Media Services</span></span>
* <span data-ttu-id="6006e-170">Engajamento Móvel</span><span class="sxs-lookup"><span data-stu-id="6006e-170">Mobile Engagement</span></span>
* <span data-ttu-id="6006e-171">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="6006e-171">Notification Hubs</span></span>
* <span data-ttu-id="6006e-172">Insights Operacionais</span><span class="sxs-lookup"><span data-stu-id="6006e-172">Operational Insights</span></span>
* <span data-ttu-id="6006e-173">Gerenciamento de Operações</span><span class="sxs-lookup"><span data-stu-id="6006e-173">Operations Management</span></span>
* <span data-ttu-id="6006e-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="6006e-174">Power BI</span></span>
* <span data-ttu-id="6006e-175">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="6006e-175">Redis Cache</span></span>
* <span data-ttu-id="6006e-176">Agendador</span><span class="sxs-lookup"><span data-stu-id="6006e-176">Scheduler</span></span>
* <span data-ttu-id="6006e-177">Search</span><span class="sxs-lookup"><span data-stu-id="6006e-177">Search</span></span>
* <span data-ttu-id="6006e-178">Gerenciamento do Servidor</span><span class="sxs-lookup"><span data-stu-id="6006e-178">Server Management</span></span>
* <span data-ttu-id="6006e-179">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="6006e-179">Service Bus</span></span>
* <span data-ttu-id="6006e-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6006e-180">Service Fabric</span></span>
* <span data-ttu-id="6006e-181">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="6006e-181">Storage</span></span>
* <span data-ttu-id="6006e-182">Armazenamento (clássico) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="6006e-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="6006e-183">Stream Analytics – os trabalhos do Stream Analytics não podem ser movidos durante o estado de execução.</span><span class="sxs-lookup"><span data-stu-id="6006e-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="6006e-184">Servidor de banco de dados do SQL - Olá banco de dados e o servidor devem residir no hello mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="6006e-185">Quando você move um SQL Server, todos os seus bancos de dados também são movidos.</span><span class="sxs-lookup"><span data-stu-id="6006e-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="6006e-186">Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="6006e-186">Traffic Manager</span></span>
* <span data-ttu-id="6006e-187">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="6006e-187">Virtual Machines</span></span>
* <span data-ttu-id="6006e-188">Máquinas virtuais com o certificado armazenado no cofre de chaves - Mover grupo de recursos de toonew na mesma assinatura é habilitada, mas a movimentação de assinatura cruzada não está habilitada.</span><span class="sxs-lookup"><span data-stu-id="6006e-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="6006e-189">Máquinas virtuais (clássicas) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="6006e-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="6006e-190">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="6006e-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="6006e-191">Redes virtuais — atualmente, uma Rede Virtual emparelhada não pode ser movida até que o emparelhamento da rede virtual tenha sido desabilitado.</span><span class="sxs-lookup"><span data-stu-id="6006e-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="6006e-192">Quando desabilitado, Olá rede Virtual pode ser movido com êxito e Olá emparelhamento de rede virtual pode ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="6006e-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="6006e-193">Além disso, uma rede Virtual não pode ser assinatura diferente tooa movido se Olá rede Virtual contém nenhuma sub-rede com links de navegação do recurso.</span><span class="sxs-lookup"><span data-stu-id="6006e-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="6006e-194">Por exemplo, uma sub-rede da Rede Virtual tem um link de navegação de recurso quando um recurso redis do Cache da Microsoft for implantado nesta sub-rede.</span><span class="sxs-lookup"><span data-stu-id="6006e-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="6006e-195">Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="6006e-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="6006e-196">Serviços que não permitem mover</span><span class="sxs-lookup"><span data-stu-id="6006e-196">Services that do not enable move</span></span>
<span data-ttu-id="6006e-197">Olá serviços que atualmente não permite mover um recurso são:</span><span class="sxs-lookup"><span data-stu-id="6006e-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="6006e-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="6006e-198">AD Domain Services</span></span>
* <span data-ttu-id="6006e-199">Serviço de Integridade Híbrida do AD</span><span class="sxs-lookup"><span data-stu-id="6006e-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="6006e-200">Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="6006e-200">Application Gateway</span></span>
* <span data-ttu-id="6006e-201">Conjuntos de disponibilidade com Máquinas Virtuais com o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6006e-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="6006e-202">Serviços do BizTalk</span><span class="sxs-lookup"><span data-stu-id="6006e-202">BizTalk Services</span></span>
* <span data-ttu-id="6006e-203">Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="6006e-203">Container Service</span></span>
* <span data-ttu-id="6006e-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6006e-204">Express Route</span></span>
* <span data-ttu-id="6006e-205">DevTest Labs - Mover grupo de recursos de toonew na mesma assinatura está habilitado, mas entre movimentação de assinatura não está habilitado.</span><span class="sxs-lookup"><span data-stu-id="6006e-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="6006e-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="6006e-206">Dynamics LCS</span></span>
* <span data-ttu-id="6006e-207">Imagens criadas no Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6006e-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="6006e-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6006e-208">Managed Disks</span></span>
* <span data-ttu-id="6006e-209">Aplicativos gerenciados</span><span class="sxs-lookup"><span data-stu-id="6006e-209">Managed Applications</span></span>
* <span data-ttu-id="6006e-210">Cofre de serviços de recuperação - também não move Olá computação, rede e armazenamento recursos associados à Olá a serviços de recuperação de cofre, consulte [limitações de serviços de recuperação](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="6006e-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="6006e-211">Segurança</span><span class="sxs-lookup"><span data-stu-id="6006e-211">Security</span></span>
* <span data-ttu-id="6006e-212">Instantâneos criados no Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6006e-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="6006e-213">Gerenciador de Dispositivos StorSimple</span><span class="sxs-lookup"><span data-stu-id="6006e-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="6006e-214">Máquinas virtuais com o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6006e-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="6006e-215">Redes Virtuais (clássicas) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="6006e-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="6006e-216">Máquinas Virtuais criadas em recursos do Marketplace — não podem ser movidas entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="6006e-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="6006e-217">Recurso precisa toobe desprovisionada na assinatura atual hello e implantada novamente na assinatura nova Olá</span><span class="sxs-lookup"><span data-stu-id="6006e-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="6006e-218">Limitações do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="6006e-218">App Service limitations</span></span>
<span data-ttu-id="6006e-219">Ao trabalhar com aplicativos do Serviço de Aplicativo, você não pode mover um plano de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6006e-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="6006e-220">aplicativos de serviço de aplicativo toomove, as opções são:</span><span class="sxs-lookup"><span data-stu-id="6006e-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="6006e-221">Mova hello plano de serviço de aplicativo e todos os outros recursos do serviço de aplicativo em que recursos tooa novo recurso de grupo que ainda não tem recursos de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6006e-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="6006e-222">Esse requisito significa que você deve mover mesmo Olá recursos do serviço de aplicativo que não estão associados com hello plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6006e-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="6006e-223">Mover grupo de recursos diferente Olá aplicativos tooa, mas manter todos os planos de serviço de aplicativo no grupo de recursos original hello.</span><span class="sxs-lookup"><span data-stu-id="6006e-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="6006e-224">Olá plano não precisa tooreside do serviço de aplicativo hello mesmo grupo de recursos aplicativo hello para Olá aplicativo toofunction corretamente.</span><span class="sxs-lookup"><span data-stu-id="6006e-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="6006e-225">Por exemplo, se o grupo de recursos contém:</span><span class="sxs-lookup"><span data-stu-id="6006e-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="6006e-226">**web-a** associado a **plan-a**</span><span class="sxs-lookup"><span data-stu-id="6006e-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="6006e-227">**web-b** associado a **plan-b**</span><span class="sxs-lookup"><span data-stu-id="6006e-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="6006e-228">Suas opções são:</span><span class="sxs-lookup"><span data-stu-id="6006e-228">Your options are:</span></span>

* <span data-ttu-id="6006e-229">Mover **web-a**, **plan-a**, **web-b** e **plan-b**</span><span class="sxs-lookup"><span data-stu-id="6006e-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="6006e-230">Mover **web-a** e **web-b**</span><span class="sxs-lookup"><span data-stu-id="6006e-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="6006e-231">Mover **web-a**</span><span class="sxs-lookup"><span data-stu-id="6006e-231">Move **web-a**</span></span>
* <span data-ttu-id="6006e-232">Mover **web-b**</span><span class="sxs-lookup"><span data-stu-id="6006e-232">Move **web-b**</span></span>

<span data-ttu-id="6006e-233">Todas as outras combinações envolvem deixar para trás um tipo de recurso que não pode ser deixado para trás ao mover um plano do Serviço de Aplicativo (qualquer tipo de recurso do Serviço de Aplicativo).</span><span class="sxs-lookup"><span data-stu-id="6006e-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="6006e-234">Se seu aplicativo web reside em um grupo de recursos diferente que seu plano de serviço de aplicativo, mas você deseja toomove ambos tooa novo grupo de recursos, você deve executar Olá mover em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="6006e-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="6006e-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6006e-235">For example:</span></span>

* <span data-ttu-id="6006e-236">**web-a** reside em **web-group**</span><span class="sxs-lookup"><span data-stu-id="6006e-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="6006e-237">**plan-a** reside em **plan-group**</span><span class="sxs-lookup"><span data-stu-id="6006e-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="6006e-238">Você deseja **web-a** e **um plano** tooreside na **grupo combinados**</span><span class="sxs-lookup"><span data-stu-id="6006e-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="6006e-239">tooaccomplish isso mover, executar duas operações de movimentação separado em Olá sequência a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="6006e-240">Mover Olá **web-a** muito**grupo de plano**</span><span class="sxs-lookup"><span data-stu-id="6006e-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="6006e-241">Mover **web-a** e **um plano** muito**grupo combinados**.</span><span class="sxs-lookup"><span data-stu-id="6006e-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="6006e-242">Você pode mover um certificado de serviço de aplicativo tooa novo grupo de recursos ou a assinatura sem problemas.</span><span class="sxs-lookup"><span data-stu-id="6006e-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="6006e-243">No entanto, se seu aplicativo da web inclui um certificado SSL que você adquiriu externamente e carregado toohello aplicativo, você deverá excluir o certificado de saudação antes de aplicativo de web móvel hello.</span><span class="sxs-lookup"><span data-stu-id="6006e-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="6006e-244">Por exemplo, você pode executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="6006e-245">Excluir o certificado de saudação carregado do aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="6006e-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="6006e-246">Mover o aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="6006e-246">Move hello web app</span></span>
3. <span data-ttu-id="6006e-247">Carregar o aplicativo web do hello certificado toohello</span><span class="sxs-lookup"><span data-stu-id="6006e-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="6006e-248">Limitações dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="6006e-248">Recovery Services limitations</span></span>
<span data-ttu-id="6006e-249">Mover não está habilitado para armazenamento, rede, ou recursos de computação usada tooset a recuperação de desastres com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6006e-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="6006e-250">Por exemplo, suponha que você configurou a replicação de sua conta de armazenamento local máquinas tooa (Storage1) e quiser Olá protegido máquina toocome backup após failover tooAzure como uma máquina virtual (VM1) anexado tooa de rede virtual (Network1).</span><span class="sxs-lookup"><span data-stu-id="6006e-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="6006e-251">Não é possível mover qualquer um desses recursos do Azure - Storage1, VM1, e Network1 - em recursos grupos dentro de saudação mesma assinatura ou em assinaturas.</span><span class="sxs-lookup"><span data-stu-id="6006e-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="6006e-252">Limitações do HDInsight</span><span class="sxs-lookup"><span data-stu-id="6006e-252">HDInsight limitations</span></span>

<span data-ttu-id="6006e-253">Você pode mover HDInsight clusters tooa nova assinatura ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="6006e-254">No entanto, você não pode mover entre Olá assinaturas à rede de cluster do HDInsight toohello vinculado recursos (como a rede virtual hello, NIC ou balanceador de carga).</span><span class="sxs-lookup"><span data-stu-id="6006e-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="6006e-255">Além disso, você não pode mover o grupo de recursos novos tooa uma NIC que é anexado tooa para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6006e-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="6006e-256">Ao mover uma assinatura de novo de tooa do cluster HDInsight, primeiro mova outros recursos (como a conta de armazenamento Olá).</span><span class="sxs-lookup"><span data-stu-id="6006e-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="6006e-257">Em seguida, mova o cluster do HDInsight Olá por si só.</span><span class="sxs-lookup"><span data-stu-id="6006e-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="6006e-258">Limitações da implantação clássica</span><span class="sxs-lookup"><span data-stu-id="6006e-258">Classic deployment limitations</span></span>
<span data-ttu-id="6006e-259">Olá a opções para mover os recursos implantados por meio do modelo clássico Olá diferem com base em se você estiver movendo recursos hello dentro de uma assinatura ou tooa nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="6006e-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="6006e-260">Mesma assinatura</span><span class="sxs-lookup"><span data-stu-id="6006e-260">Same subscription</span></span>
<span data-ttu-id="6006e-261">Ao mover os recursos do grupo de recursos de tooanother de grupo de um recurso dentro Olá a mesma assinatura, Olá restrições a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="6006e-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="6006e-262">Redes virtuais (clássicas) não podem ser movidas.</span><span class="sxs-lookup"><span data-stu-id="6006e-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="6006e-263">Máquinas virtuais (clássicas) devem ser movidas com o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6006e-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="6006e-264">Serviço de nuvem pode ser movido apenas quando mover Olá inclui todas as suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6006e-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="6006e-265">Apenas um serviço de nuvem pode ser movido por vez.</span><span class="sxs-lookup"><span data-stu-id="6006e-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="6006e-266">Apenas uma conta de armazenamento (clássica) pode ser movida por vez.</span><span class="sxs-lookup"><span data-stu-id="6006e-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="6006e-267">Conta de armazenamento (clássico) não pode ser movida em Olá mesma operação com uma máquina virtual ou um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6006e-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="6006e-268">toomove recursos clássicos tooa novo grupo de recursos dentro Olá a mesma assinatura, use operações de movimentação padrão Olá por meio de saudação [portal](#use-portal), [Azure PowerShell](#use-powershell), [CLI do Azure](#use-azure-cli), ou [API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="6006e-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="6006e-269">Você usa Olá mesmas operações que você usa para mover os recursos do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="6006e-270">Nova assinatura</span><span class="sxs-lookup"><span data-stu-id="6006e-270">New subscription</span></span>
<span data-ttu-id="6006e-271">Ao mover a nova assinatura de recursos de tooa, Olá restrições a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="6006e-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="6006e-272">Todos os recursos clássicos na assinatura Olá devem ser movidos no hello mesma operação.</span><span class="sxs-lookup"><span data-stu-id="6006e-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="6006e-273">assinatura de destino Olá não deve conter todos os outros recursos clássicos.</span><span class="sxs-lookup"><span data-stu-id="6006e-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="6006e-274">Olá move pode ser solicitado somente por meio de uma API REST separado para move clássico.</span><span class="sxs-lookup"><span data-stu-id="6006e-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="6006e-275">comandos de movimentação do Gerenciador de recursos padrão Olá não funcionam quando mover recursos clássicos tooa nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="6006e-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="6006e-276">toomove recursos clássicos tooa nova assinatura, use Olá REST operações recursos tooclassic específico.</span><span class="sxs-lookup"><span data-stu-id="6006e-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="6006e-277">toouse REST, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="6006e-278">Verifique se a assinatura de origem Olá pode participar de uma assinatura entre mover.</span><span class="sxs-lookup"><span data-stu-id="6006e-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="6006e-279">Use Olá operação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="6006e-280">No corpo da solicitação de hello, incluem:</span><span class="sxs-lookup"><span data-stu-id="6006e-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="6006e-281">resposta de saudação para operação de validação hello está no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="6006e-282">Verifique se a assinatura de destino Olá pode participar de uma assinatura cruzada mover.</span><span class="sxs-lookup"><span data-stu-id="6006e-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="6006e-283">Use Olá operação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="6006e-284">No corpo da solicitação de hello, incluem:</span><span class="sxs-lookup"><span data-stu-id="6006e-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="6006e-285">resposta de saudação está no hello mesmo formato que a validação de assinatura de origem hello.</span><span class="sxs-lookup"><span data-stu-id="6006e-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="6006e-286">Se as duas assinaturas passarem na validação, mova todos os recursos clássicos de assinatura de tooanother de uma assinatura com hello operação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="6006e-287">No corpo da solicitação de hello, incluem:</span><span class="sxs-lookup"><span data-stu-id="6006e-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="6006e-288">operação de saudação pode ser executada por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="6006e-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="6006e-289">Usar o portal</span><span class="sxs-lookup"><span data-stu-id="6006e-289">Use portal</span></span>
<span data-ttu-id="6006e-290">toomove recursos, selecione grupo de recursos de saudação contendo esses recursos e selecione Olá **mover** botão.</span><span class="sxs-lookup"><span data-stu-id="6006e-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Mover recursos](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="6006e-292">Selecione se você estiver movendo Olá recursos tooa novo grupo de recursos ou uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="6006e-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="6006e-293">Selecione Olá recursos toomove e o grupo de recursos de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="6006e-294">Confirmar que você precisa tooupdate scripts para esses recursos e selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6006e-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="6006e-295">Se você selecionou o ícone de assinatura de edição de saudação na etapa anterior Olá, você também deve selecionar a assinatura de destino hello.</span><span class="sxs-lookup"><span data-stu-id="6006e-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![selecionar destino](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="6006e-297">Em **notificações**, você verá que Olá mover a operação está em execução.</span><span class="sxs-lookup"><span data-stu-id="6006e-297">In **Notifications**, you see that hello move operation is running.</span></span>

![mostrar status da movimentação](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="6006e-299">Quando ele for concluído, você será notificado de resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="6006e-299">When it has completed, you are notified of hello result.</span></span>

![mostrar resultado da movimentação](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="6006e-301">Usar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6006e-301">Use PowerShell</span></span>
<span data-ttu-id="6006e-302">toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá `Move-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="6006e-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="6006e-303">Olá primeiro exemplo mostra como toomove um recurso tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="6006e-304">Olá segundo exemplo mostra como toomove vários recursos tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="6006e-305">toomove tooa nova assinatura, inclua um valor para Olá `DestinationSubscriptionId` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6006e-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="6006e-306">Você será solicitado tooconfirm que você deseja toomove Olá especificado recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="6006e-307">Usar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6006e-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="6006e-308">toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá `az resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="6006e-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="6006e-309">Fornece recursos Olá IDs de saudação recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="6006e-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="6006e-310">Você pode obter IDs de recurso com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="6006e-311">saudação de exemplo a seguir mostra como a conta toomove um armazenamento tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="6006e-312">Em Olá `--ids` parâmetro, forneça uma lista separada de saudação toomove de IDs de recurso.</span><span class="sxs-lookup"><span data-stu-id="6006e-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="6006e-313">toomove tooa nova assinatura, forneça Olá `--destination-subscription-id` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6006e-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="6006e-314">Usar a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6006e-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="6006e-315">toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá `azure resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="6006e-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="6006e-316">Fornece recursos Olá IDs de saudação recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="6006e-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="6006e-317">Você pode obter IDs de recurso com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="6006e-318">Que retorna Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="6006e-318">Which returns hello following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="6006e-319">saudação de exemplo a seguir mostra como a conta toomove um armazenamento tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6006e-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="6006e-320">Em Olá `-i` parâmetro, fornecer uma lista separada por vírgulas de saudação toomove de IDs de recurso.</span><span class="sxs-lookup"><span data-stu-id="6006e-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="6006e-321">Você será solicitado tooconfirm que você deseja toomove Olá o recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="6006e-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="6006e-322">Usar a API REST</span><span class="sxs-lookup"><span data-stu-id="6006e-322">Use REST API</span></span>
<span data-ttu-id="6006e-323">grupo de recursos para toomove existente recursos tooanother ou assinatura, execute:</span><span class="sxs-lookup"><span data-stu-id="6006e-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="6006e-324">No corpo da solicitação de Olá, especifique o grupo de recursos de destino hello e Olá recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="6006e-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="6006e-325">Para obter mais informações sobre a operação de REST de movimentação hello, consulte [mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="6006e-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6006e-326">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6006e-326">Next steps</span></span>
* <span data-ttu-id="6006e-327">toolearn sobre cmdlets do PowerShell para gerenciar sua assinatura, consulte [usando o PowerShell do Azure com o Gerenciador de recursos](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="6006e-328">toolearn sobre comandos de CLI do Azure para gerenciar sua assinatura, consulte [hello usando a CLI do Azure com o Gerenciador de recursos](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="6006e-329">toolearn sobre recursos do portal para gerenciar sua assinatura, consulte [usando os recursos do Azure toomanage portal Olá](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="6006e-330">toolearn sobre a aplicação de recursos de tooyour uma organização lógica, consulte [usando marcas tooorganize seus recursos](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="6006e-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
