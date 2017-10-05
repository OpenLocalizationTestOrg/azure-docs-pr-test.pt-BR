---
title: Mover recursos do Azure para uma nova assinatura ou um novo grupo de recursos | Microsoft Docs
description: Use o Azure Resource Manager para mover recursos para um novo grupo de recursos ou uma nova assinatura.
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
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="8ccdc-103">Mover recursos para um novo grupo de recursos ou uma nova assinatura</span><span class="sxs-lookup"><span data-stu-id="8ccdc-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="8ccdc-104">Este tópico mostra como mover recursos para uma nova assinatura ou um novo grupo de recursos na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="8ccdc-105">Você pode usar o portal, PowerShell, CLI do Azure ou a API REST para mover recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="8ccdc-106">As operações de movimentação neste tópico estão disponíveis para você sem nenhuma assistência do suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="8ccdc-107">O grupo de origem e o grupo de destino ficam bloqueados durante a operação de movimentação de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="8ccdc-108">As operações de gravação e exclusão são bloqueadas nos grupos de recursos até que a migração seja concluída.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="8ccdc-109">Esse bloqueio significa que você não pode adicionar, atualizar nem excluir os recursos nos grupos de recursos, mas isso não significa que os recursos estão congelados.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="8ccdc-110">Por exemplo, se você mover um SQL Server e seu banco de dados para um novo grupo de recursos, um aplicativo que usa o banco de dados não terá nenhuma inatividade.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="8ccdc-111">Ele ainda poderá ler e gravar no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-111">It can still read and write to the database.</span></span>

<span data-ttu-id="8ccdc-112">Você não pode alterar o local do recurso.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="8ccdc-113">Mover um recurso só o move para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="8ccdc-114">O novo grupo de recursos pode ter um local diferente, mas que não altere o local do recurso.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="8ccdc-115">Este artigo descreve como mover recursos dentro de uma oferta de conta existente do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="8ccdc-116">Se você realmente deseja alterar sua oferta de conta do Azure (por exemplo, atualizando do modo pré-pago para pagar antecipadamente), mas quer continuar trabalhando com seus recursos existentes, consulte [Trocar a assinatura do Azure por outra oferta](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="8ccdc-117">Lista de verificação antes de mover recursos</span><span class="sxs-lookup"><span data-stu-id="8ccdc-117">Checklist before moving resources</span></span>
<span data-ttu-id="8ccdc-118">Há algumas etapas importantes a serem realizadas antes de mover um recurso.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="8ccdc-119">Ao verificar essas condições, é possível evitar erros.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="8ccdc-120">As assinaturas de origem e de destino devem existir no mesmo [locatário do Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="8ccdc-121">Para verificar se as duas assinaturas têm a mesma ID de locatário, use o Azure PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="8ccdc-122">Para o Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="8ccdc-123">Para a CLI 2.0 do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="8ccdc-124">Se as IDs do locatário para as assinaturas de origem e de destino não forem iguais, tente alterar o diretório da assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="8ccdc-125">No entanto, essa opção só está disponível para Administradores de Serviço conectados a uma conta da Microsoft (e não uma conta corporativa).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="8ccdc-126">Para tentar alterar o diretório, faça logon no [portal clássico](https://manage.windowsazure.com/) e selecione **Configurações** para selecionar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="8ccdc-127">Se o ícone **Editar Diretório** estiver disponível, selecione-o para alterar o Azure Active Directory associado.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![editar diretório](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="8ccdc-129">Se esse ícone não estiver disponível, será necessário entrar em contato com o suporte para mover os recursos para um novo locatário.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="8ccdc-130">O serviço deve permitir a movimentação de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="8ccdc-131">Este tópico lista quais serviços permitem mover os recursos e quais serviços não habilitam a movimentação dos recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="8ccdc-132">A assinatura de destino deve estar registrada para que o provedor de recursos do recurso seja movido.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="8ccdc-133">Se não estiver, você receberá um erro afirmando que a **assinatura não está registrada para um tipo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="8ccdc-134">Você pode encontrar esse problema ao mover um recurso para uma nova assinatura que nunca tenha sido usada com esse tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="8ccdc-135">Para saber como verificar o status do registro e registrar provedores de recursos, consulte [Provedores e tipos de recursos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="8ccdc-136">Quando telefonar para o suporte</span><span class="sxs-lookup"><span data-stu-id="8ccdc-136">When to call support</span></span>
<span data-ttu-id="8ccdc-137">Você pode mover a maioria dos recursos por meio de operações de autoatendimento mostradas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="8ccdc-138">Use as operações de autoatendimento para:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="8ccdc-139">Mova os recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="8ccdc-140">Mover recursos clássicos de acordo com as [Limitações da implantação clássica](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="8ccdc-141">Telefonar para o suporte quando você precisa:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-141">Call support when you need to:</span></span>

* <span data-ttu-id="8ccdc-142">Mova os recursos para uma nova conta do Azure (e locatário do Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="8ccdc-143">Mover recursos clássicos, mas está tendo problemas com as limitações.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="8ccdc-144">Serviços que permitem mover</span><span class="sxs-lookup"><span data-stu-id="8ccdc-144">Services that enable move</span></span>
<span data-ttu-id="8ccdc-145">Por enquanto, os serviços que permitem mover para um novo grupo de recursos e uma nova assinatura são:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="8ccdc-146">Gerenciamento da API</span><span class="sxs-lookup"><span data-stu-id="8ccdc-146">API Management</span></span>
* <span data-ttu-id="8ccdc-147">Aplicativos do Serviço de Aplicativo (aplicativos Web) - consulte [Limitações do Serviço de Aplicativo](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="8ccdc-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="8ccdc-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ccdc-148">Application Insights</span></span>
* <span data-ttu-id="8ccdc-149">Automação</span><span class="sxs-lookup"><span data-stu-id="8ccdc-149">Automation</span></span>
* <span data-ttu-id="8ccdc-150">Batch</span><span class="sxs-lookup"><span data-stu-id="8ccdc-150">Batch</span></span>
* <span data-ttu-id="8ccdc-151">Bing Mapas</span><span class="sxs-lookup"><span data-stu-id="8ccdc-151">Bing Maps</span></span>
* <span data-ttu-id="8ccdc-152">CDN</span><span class="sxs-lookup"><span data-stu-id="8ccdc-152">CDN</span></span>
* <span data-ttu-id="8ccdc-153">Serviços de Nuvem - veja [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8ccdc-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8ccdc-154">Serviços Cognitivos</span><span class="sxs-lookup"><span data-stu-id="8ccdc-154">Cognitive Services</span></span>
* <span data-ttu-id="8ccdc-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="8ccdc-155">Content Moderator</span></span>
* <span data-ttu-id="8ccdc-156">Catálogo de Dados</span><span class="sxs-lookup"><span data-stu-id="8ccdc-156">Data Catalog</span></span>
* <span data-ttu-id="8ccdc-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="8ccdc-157">Data Factory</span></span>
* <span data-ttu-id="8ccdc-158">Análises Data Lake</span><span class="sxs-lookup"><span data-stu-id="8ccdc-158">Data Lake Analytics</span></span>
* <span data-ttu-id="8ccdc-159">Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="8ccdc-159">Data Lake Store</span></span>
* <span data-ttu-id="8ccdc-160">DNS</span><span class="sxs-lookup"><span data-stu-id="8ccdc-160">DNS</span></span>
* <span data-ttu-id="8ccdc-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ccdc-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="8ccdc-162">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="8ccdc-162">Event Hubs</span></span>
* <span data-ttu-id="8ccdc-163">Clusters HDInsight – veja [Limitações do HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="8ccdc-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="8ccdc-164">Hubs IoT</span><span class="sxs-lookup"><span data-stu-id="8ccdc-164">IoT Hubs</span></span>
* <span data-ttu-id="8ccdc-165">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="8ccdc-165">Key Vault</span></span>
* <span data-ttu-id="8ccdc-166">Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="8ccdc-166">Load Balancers</span></span>
* <span data-ttu-id="8ccdc-167">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="8ccdc-167">Logic Apps</span></span>
* <span data-ttu-id="8ccdc-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8ccdc-168">Machine Learning</span></span>
* <span data-ttu-id="8ccdc-169">Serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="8ccdc-169">Media Services</span></span>
* <span data-ttu-id="8ccdc-170">Engajamento Móvel</span><span class="sxs-lookup"><span data-stu-id="8ccdc-170">Mobile Engagement</span></span>
* <span data-ttu-id="8ccdc-171">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="8ccdc-171">Notification Hubs</span></span>
* <span data-ttu-id="8ccdc-172">Insights Operacionais</span><span class="sxs-lookup"><span data-stu-id="8ccdc-172">Operational Insights</span></span>
* <span data-ttu-id="8ccdc-173">Gerenciamento de Operações</span><span class="sxs-lookup"><span data-stu-id="8ccdc-173">Operations Management</span></span>
* <span data-ttu-id="8ccdc-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="8ccdc-174">Power BI</span></span>
* <span data-ttu-id="8ccdc-175">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="8ccdc-175">Redis Cache</span></span>
* <span data-ttu-id="8ccdc-176">Agendador</span><span class="sxs-lookup"><span data-stu-id="8ccdc-176">Scheduler</span></span>
* <span data-ttu-id="8ccdc-177">Search</span><span class="sxs-lookup"><span data-stu-id="8ccdc-177">Search</span></span>
* <span data-ttu-id="8ccdc-178">Gerenciamento do Servidor</span><span class="sxs-lookup"><span data-stu-id="8ccdc-178">Server Management</span></span>
* <span data-ttu-id="8ccdc-179">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="8ccdc-179">Service Bus</span></span>
* <span data-ttu-id="8ccdc-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ccdc-180">Service Fabric</span></span>
* <span data-ttu-id="8ccdc-181">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="8ccdc-181">Storage</span></span>
* <span data-ttu-id="8ccdc-182">Armazenamento (clássico) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8ccdc-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8ccdc-183">Stream Analytics – os trabalhos do Stream Analytics não podem ser movidos durante o estado de execução.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="8ccdc-184">Servidor do Banco de Dados SQL - O banco de dados e o servidor devem residir no mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="8ccdc-185">Quando você move um SQL Server, todos os seus bancos de dados também são movidos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="8ccdc-186">Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="8ccdc-186">Traffic Manager</span></span>
* <span data-ttu-id="8ccdc-187">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="8ccdc-187">Virtual Machines</span></span>
* <span data-ttu-id="8ccdc-188">As Máquinas virtuais com certificado armazenado no Key Vault – Se deslocam para um novo grupo de recursos na mesma assinatura em que foram habilitadas, porém, o deslocamento para uma assinatura cruzada não é habilitada.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="8ccdc-189">Máquinas virtuais (clássicas) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8ccdc-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8ccdc-190">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="8ccdc-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="8ccdc-191">Redes virtuais — atualmente, uma Rede Virtual emparelhada não pode ser movida até que o emparelhamento da rede virtual tenha sido desabilitado.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="8ccdc-192">Depois de desabilitado, a Rede Virtual pode ser movida com êxito e o emparelhamento VNet pode ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="8ccdc-193">Além disso, uma Rede Virtual não pode ser deslocada para uma assinatura diferente caso a Rede Virtual contenha qualquer sub-rede com links de navegação de recurso.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="8ccdc-194">Por exemplo, uma sub-rede da Rede Virtual tem um link de navegação de recurso quando um recurso redis do Cache da Microsoft for implantado nesta sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="8ccdc-195">Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="8ccdc-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="8ccdc-196">Serviços que não permitem mover</span><span class="sxs-lookup"><span data-stu-id="8ccdc-196">Services that do not enable move</span></span>
<span data-ttu-id="8ccdc-197">Os serviços que atualmente não permitem mover um recurso são:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="8ccdc-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="8ccdc-198">AD Domain Services</span></span>
* <span data-ttu-id="8ccdc-199">Serviço de Integridade Híbrida do AD</span><span class="sxs-lookup"><span data-stu-id="8ccdc-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="8ccdc-200">Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8ccdc-200">Application Gateway</span></span>
* <span data-ttu-id="8ccdc-201">Conjuntos de disponibilidade com Máquinas Virtuais com o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8ccdc-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="8ccdc-202">Serviços do BizTalk</span><span class="sxs-lookup"><span data-stu-id="8ccdc-202">BizTalk Services</span></span>
* <span data-ttu-id="8ccdc-203">Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="8ccdc-203">Container Service</span></span>
* <span data-ttu-id="8ccdc-204">Rota Expressa</span><span class="sxs-lookup"><span data-stu-id="8ccdc-204">Express Route</span></span>
* <span data-ttu-id="8ccdc-205">Laboratórios DevTest – Habilita a mudança para um novo grupo de recursos na mesma assinatura, mas desabilita a troca entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="8ccdc-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="8ccdc-206">Dynamics LCS</span></span>
* <span data-ttu-id="8ccdc-207">Imagens criadas no Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8ccdc-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="8ccdc-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8ccdc-208">Managed Disks</span></span>
* <span data-ttu-id="8ccdc-209">Aplicativos gerenciados</span><span class="sxs-lookup"><span data-stu-id="8ccdc-209">Managed Applications</span></span>
* <span data-ttu-id="8ccdc-210">Cofre de Serviços de Recuperação – não mova os recursos de Computação, Rede e Armazenamento associados ao cofre dos Serviços de Recuperação. Consulte [Limitações dos Serviços de Recuperação](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="8ccdc-211">Segurança</span><span class="sxs-lookup"><span data-stu-id="8ccdc-211">Security</span></span>
* <span data-ttu-id="8ccdc-212">Instantâneos criados no Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8ccdc-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="8ccdc-213">Gerenciador de Dispositivos StorSimple</span><span class="sxs-lookup"><span data-stu-id="8ccdc-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="8ccdc-214">Máquinas virtuais com o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8ccdc-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="8ccdc-215">Redes Virtuais (clássicas) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8ccdc-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8ccdc-216">Máquinas Virtuais criadas em recursos do Marketplace — não podem ser movidas entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="8ccdc-217">O recurso precisa ser desprovisionado na assinatura atual e implantado novamente na nova assinatura</span><span class="sxs-lookup"><span data-stu-id="8ccdc-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="8ccdc-218">Limitações do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8ccdc-218">App Service limitations</span></span>
<span data-ttu-id="8ccdc-219">Ao trabalhar com aplicativos do Serviço de Aplicativo, você não pode mover um plano de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="8ccdc-220">Para mover os Aplicativos do Serviço de Aplicativo, as opções são:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="8ccdc-221">Mova o plano do Serviço de Aplicativo e todos os outros recursos do Serviço de Aplicativo nesse grupo de recursos para um novo grupo de recursos que ainda não têm os recursos do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="8ccdc-222">Esse requisito significa que você precisa mover até mesmo os recursos do Serviço de Aplicativo que não estão associados ao plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="8ccdc-223">Mova os aplicativos para um grupo de recursos diferente, mas mantenha todos os planos do Serviço de Aplicativo no grupo de recursos original.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="8ccdc-224">O Plano do Serviço de Aplicativo não precisa residir no mesmo grupo de recursos que o aplicativo para que o aplicativo funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="8ccdc-225">Por exemplo, se o grupo de recursos contém:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="8ccdc-226">**web-a** associado a **plan-a**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="8ccdc-227">**web-b** associado a **plan-b**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="8ccdc-228">Suas opções são:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-228">Your options are:</span></span>

* <span data-ttu-id="8ccdc-229">Mover **web-a**, **plan-a**, **web-b** e **plan-b**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="8ccdc-230">Mover **web-a** e **web-b**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="8ccdc-231">Mover **web-a**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-231">Move **web-a**</span></span>
* <span data-ttu-id="8ccdc-232">Mover **web-b**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-232">Move **web-b**</span></span>

<span data-ttu-id="8ccdc-233">Todas as outras combinações envolvem deixar para trás um tipo de recurso que não pode ser deixado para trás ao mover um plano do Serviço de Aplicativo (qualquer tipo de recurso do Serviço de Aplicativo).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="8ccdc-234">Caso o aplicativo Web resida em um grupo de recursos diferente de seu plano do Serviço de Aplicativo, mas você desejar mover ambos para um novo grupo de recursos, será necessário realizar a movimentação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="8ccdc-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-235">For example:</span></span>

* <span data-ttu-id="8ccdc-236">**web-a** reside em **web-group**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="8ccdc-237">**plan-a** reside em **plan-group**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="8ccdc-238">Você quer que **web-a** e **plan-a** residam em **combined-group**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="8ccdc-239">Para realizar essa movimentação, execute duas operações de movimentação separadas na sequência a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="8ccdc-240">Mover **web-a** para **plan-group**</span><span class="sxs-lookup"><span data-stu-id="8ccdc-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="8ccdc-241">Mover **web-a** e **plan-a** para **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="8ccdc-242">Você pode mover um Certificado do Serviço de Aplicativo para um novo grupo de recursos ou assinatura sem problemas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="8ccdc-243">No entanto, se seu aplicativo Web incluir um certificado SSL que você tiver comprado externamente e carregado para o aplicativo, você deverá excluir o certificado antes de mover o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="8ccdc-244">Por exemplo, você pode executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="8ccdc-245">Excluir o certificado carregado do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8ccdc-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="8ccdc-246">Mover o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8ccdc-246">Move the web app</span></span>
3. <span data-ttu-id="8ccdc-247">Carregar o certificado no aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8ccdc-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="8ccdc-248">Limitações dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="8ccdc-248">Recovery Services limitations</span></span>
<span data-ttu-id="8ccdc-249">A movimentação dos recursos de Armazenamento, Rede ou Computação usados para configurar a recuperação de desastres com o Azure Site Recovery não está habilitada.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="8ccdc-250">Por exemplo, suponha que você configurou a replicação das máquinas locais para uma conta de armazenamento (Storage1) e queira que a máquina protegida venha, após o failover, para o Azure como uma máquina virtual (VM1) conectada a uma rede virtual (Network1).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="8ccdc-251">Você não pode mover nenhum desses recursos do Azure – Storage1, VM1 e Network1 – entre grupos de recursos dentro da mesma assinatura ou em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="8ccdc-252">Limitações do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ccdc-252">HDInsight limitations</span></span>

<span data-ttu-id="8ccdc-253">Você pode mover os clusters HDInsight para uma nova assinatura ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="8ccdc-254">No entanto, não é possível mover os recursos de rede vinculados ao cluster HDInsight (por exemplo, a rede virtual, NIC ou balanceador de carga) entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="8ccdc-255">Além disso, não é possível mover uma para um novo grupo de recursos uma NIC que está conectada a uma máquina virtual para o cluster.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="8ccdc-256">Ao mover um cluster HDInsight para uma nova assinatura, mova primeiro os outros recursos (como a conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="8ccdc-257">Em seguida, mova apenas o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="8ccdc-258">Limitações da implantação clássica</span><span class="sxs-lookup"><span data-stu-id="8ccdc-258">Classic deployment limitations</span></span>
<span data-ttu-id="8ccdc-259">As opções de movimentação dos recursos implantados por meio do modelo clássico apesentam diferenças, dependendo se você estiver movendo os recursos em uma assinatura ou para uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="8ccdc-260">Mesma assinatura</span><span class="sxs-lookup"><span data-stu-id="8ccdc-260">Same subscription</span></span>
<span data-ttu-id="8ccdc-261">Ao mover recursos de um grupo de recursos para outro na mesma assinatura, as seguintes restrições se aplicarão:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="8ccdc-262">Redes virtuais (clássicas) não podem ser movidas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="8ccdc-263">Máquinas virtuais (clássicas) devem ser movidas com o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="8ccdc-264">Um serviço de nuvem pode ser movido apenas quando a movimentação incluir todas as suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="8ccdc-265">Apenas um serviço de nuvem pode ser movido por vez.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="8ccdc-266">Apenas uma conta de armazenamento (clássica) pode ser movida por vez.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="8ccdc-267">Uma conta de armazenamento (clássica) não pode ser movida na mesma operação com uma máquina virtual ou um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="8ccdc-268">Para mover recursos clássicos para um novo grupo de recursos dentro da mesma assinatura, use o [portal](#use-portal), o [Azure PowerShell](#use-powershell), a [CLI do Azure](#use-azure-cli) ou a [API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="8ccdc-269">Use as mesmas operações como você usa para mover os recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="8ccdc-270">Nova assinatura</span><span class="sxs-lookup"><span data-stu-id="8ccdc-270">New subscription</span></span>
<span data-ttu-id="8ccdc-271">Ao mover recursos para uma nova assinatura, as seguintes restrições se aplicarão:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="8ccdc-272">Todos os recursos clássicos na assinatura devem ser movidos na mesma operação.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="8ccdc-273">A assinatura de destino não deve conter nenhum outro recurso clássico.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="8ccdc-274">A movimentação pode ser solicitada apenas por meio de uma API REST separada para movimentações clássicas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="8ccdc-275">Os comandos de movimentação padrão do Gerenciador de Recursos não funcionam quando há uma movimentação dos recursos clássicos para uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="8ccdc-276">Para mover recursos clássicos para uma nova assinatura, use operações REST específicas para recursos clássicos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="8ccdc-277">Para usar REST, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="8ccdc-278">Verifique se a assinatura de origem pode participar de uma movimentação entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="8ccdc-279">Use a operação a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="8ccdc-280">No corpo da solicitação, inclua:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="8ccdc-281">A resposta para a operação de validação é no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="8ccdc-282">Verifique se a assinatura de destino pode participar de uma movimentação entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="8ccdc-283">Use a operação a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="8ccdc-284">No corpo da solicitação, inclua:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="8ccdc-285">A resposta está no mesmo formato que a validação de assinatura de origem.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="8ccdc-286">Se ambas as assinaturas forem aprovadas na validação, mova todos os recursos clássicos de uma assinatura para outra, use a seguinte operação:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="8ccdc-287">No corpo da solicitação, inclua:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="8ccdc-288">A operação pode executar por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="8ccdc-289">Usar o portal</span><span class="sxs-lookup"><span data-stu-id="8ccdc-289">Use portal</span></span>
<span data-ttu-id="8ccdc-290">Para mover recursos, selecione o grupo de recursos que os contém e, em seguida, o botão **Mover**.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Mover recursos](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="8ccdc-292">Selecione se você está movendo os recursos para um novo grupo de recursos ou para uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="8ccdc-293">Selecione os recursos a serem movidos e o grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="8ccdc-294">Confirme que você precisa atualizar scripts para esses recursos e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="8ccdc-295">Se tiver selecionado o ícone de edição da assinatura na etapa anterior, você também precisará selecionar a assinatura de destino.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![selecionar destino](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="8ccdc-297">Em **Notificações**, você verá que a operação de movimentação está em execução.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-297">In **Notifications**, you see that the move operation is running.</span></span>

![mostrar status da movimentação](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="8ccdc-299">Quando for concluída, você será notificado sobre o resultado.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-299">When it has completed, you are notified of the result.</span></span>

![mostrar resultado da movimentação](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="8ccdc-301">Usar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ccdc-301">Use PowerShell</span></span>
<span data-ttu-id="8ccdc-302">Para mover recursos existentes para outro grupo de recursos ou assinatura, use o comando `Move-AzureRmResource`.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="8ccdc-303">O primeiro exemplo mostra como mover um recurso para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="8ccdc-304">O segundo exemplo mostra como mover vários recursos para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="8ccdc-305">Para mover para uma nova assinatura, inclua um valor para o parâmetro `DestinationSubscriptionId`.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="8ccdc-306">Será solicitado que você confirme que deseja mover os recursos especificados.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="8ccdc-307">Usar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8ccdc-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="8ccdc-308">Para mover recursos existentes para outro grupo de recursos ou assinatura, use o comando `az resource move`.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="8ccdc-309">Forneça as IDs dos recursos a mover.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="8ccdc-310">Você pode obter as IDs dos recursos com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="8ccdc-311">O exemplo a seguir mostra como mover uma conta de armazenamento para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="8ccdc-312">No parâmetro `--ids`, forneça uma lista separada por espaços das IDs do recurso que deseja mover.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="8ccdc-313">Para mover para uma nova assinatura, forneça o parâmetro `--destination-subscription-id`.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="8ccdc-314">Usar a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8ccdc-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="8ccdc-315">Para mover recursos existentes para outro grupo de recursos ou assinatura, use o comando `azure resource move`.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="8ccdc-316">Forneça as IDs dos recursos a mover.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="8ccdc-317">Você pode obter as IDs dos recursos com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="8ccdc-318">Isso retorna o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-318">Which returns the following format:</span></span>

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

<span data-ttu-id="8ccdc-319">O exemplo a seguir mostra como mover uma conta de armazenamento para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="8ccdc-320">No parâmetro `-i`, forneça uma lista separada por vírgulas das IDs do recurso que deseja mover.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="8ccdc-321">Será solicitado que você confirme que deseja mover o recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="8ccdc-322">Usar a API REST</span><span class="sxs-lookup"><span data-stu-id="8ccdc-322">Use REST API</span></span>
<span data-ttu-id="8ccdc-323">Para mover recursos existentes para outro grupo de recursos ou outra assinatura, execute:</span><span class="sxs-lookup"><span data-stu-id="8ccdc-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="8ccdc-324">No corpo da solicitação, especifique o grupo de recursos de destino e os recursos para mover.</span><span class="sxs-lookup"><span data-stu-id="8ccdc-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="8ccdc-325">Para obter mais informações sobre a operação de movimentação REST, consulte [Mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ccdc-326">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ccdc-326">Next steps</span></span>
* <span data-ttu-id="8ccdc-327">Para saber mais sobre os cmdlets do PowerShell para gerenciar sua assinatura, veja [Como usar o Azure PowerShell com o Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="8ccdc-328">Para saber mais sobre os comandos da CLI do Azure para gerenciar sua assinatura, veja [Como usar a CLI do Azure com o Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="8ccdc-329">Para saber mais sobre os recursos do portal para gerenciar sua assinatura, veja [Usar o Portal do Azure para gerenciar recursos](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="8ccdc-330">Para saber mais sobre como aplicar uma organização lógica aos seus recursos, veja [Usando marcações para organizar seus recursos](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="8ccdc-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
