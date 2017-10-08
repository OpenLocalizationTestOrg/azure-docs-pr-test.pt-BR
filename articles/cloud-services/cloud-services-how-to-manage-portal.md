---
title: "tarefas de gerenciamento de serviço de nuvem aaaCommon | Microsoft Docs"
description: "Saiba como os serviços de nuvem toomanage em Olá portal do Azure. Esses exemplos usam Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="47f93-104">Como os serviços de nuvem tooManage</span><span class="sxs-lookup"><span data-stu-id="47f93-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47f93-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="47f93-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="47f93-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="47f93-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="47f93-107">Em Olá **serviços de nuvem (clássicos)** área de hello Azure portal, você pode atualizar uma função de serviço ou uma implantação, promover uma implantação de preparo tooproduction, vincular o serviço de nuvem tooyour recursos para que você possa ver recursos Olá dependências e escala Olá recursos juntos e excluir um serviço de nuvem ou uma implantação.</span><span class="sxs-lookup"><span data-stu-id="47f93-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="47f93-108">Para obter mais informações sobre como tooscale seu serviço de nuvem está disponível [aqui](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="47f93-109">Como atualizar uma função ou implantação de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="47f93-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="47f93-110">Se precisar de código do aplicativo hello tooupdate para seu serviço de nuvem, use **atualização** na folha de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="47f93-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="47f93-111">Você pode atualizar única função ou todas as funções.</span><span class="sxs-lookup"><span data-stu-id="47f93-111">You can update a single role or all roles.</span></span> <span data-ttu-id="47f93-112">tooupdate, você pode carregar um novo pacote de serviço ou o arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="47f93-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="47f93-113">Em Olá [portal do Azure][Azure portal], selecione Serviço de nuvem Olá tooupdate desejado.</span><span class="sxs-lookup"><span data-stu-id="47f93-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="47f93-114">Essa etapa abre a folha de instância de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="47f93-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="47f93-115">Na folha de saudação, clique em Olá **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="47f93-115">In hello blade, click hello **Update** button.</span></span>

    ![Botão Atualizar](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="47f93-117">Atualize implantação Olá com um novo arquivo de pacote de serviço (. cspkg) e o arquivo de configuração de serviço (. cscfg).</span><span class="sxs-lookup"><span data-stu-id="47f93-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="47f93-119">**Opcionalmente,** atualizar o rótulo de implantação hello e conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="47f93-120">Se nenhuma função tiver apenas uma instância de função, selecione Olá **implantar mesmo se uma ou mais funções contiverem uma única instância** tooenable Olá atualização tooproceed.</span><span class="sxs-lookup"><span data-stu-id="47f93-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="47f93-121">O Azure pode garantir apenas 99,95 por cento de disponibilidade do Serviço de Nuvem durante uma atualização do Serviço de Nuvem se cada função tiver pelo menos duas instâncias de função (máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="47f93-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="47f93-122">Com duas instâncias de função, uma máquina virtual processa solicitações de cliente, enquanto outros hello está atualizada.</span><span class="sxs-lookup"><span data-stu-id="47f93-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="47f93-123">Verificar **comece** toohave atualização de saudação aplicada após o término hello carregamento do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="47f93-124">Clique em **Okey** toobegin atualização Olá service.</span><span class="sxs-lookup"><span data-stu-id="47f93-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="47f93-125">Como: alternar implantações toopromote tooproduction uma implantação de preparo</span><span class="sxs-lookup"><span data-stu-id="47f93-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="47f93-126">Quando você decide toodeploy uma nova versão de um serviço de nuvem, estágio e testar a nova versão em seu ambiente de preparo de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="47f93-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="47f93-127">Use **trocar** tooswitch Olá URLs por quais Olá duas implantações são endereçadas e promovem um novo tooproduction de versão.</span><span class="sxs-lookup"><span data-stu-id="47f93-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="47f93-128">Você pode alternar as implantações de saudação **serviços de nuvem** painel de página ou hello.</span><span class="sxs-lookup"><span data-stu-id="47f93-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="47f93-129">Em Olá [portal do Azure][Azure portal], selecione Serviço de nuvem Olá tooupdate desejado.</span><span class="sxs-lookup"><span data-stu-id="47f93-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="47f93-130">Essa etapa abre a folha de instância de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="47f93-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="47f93-131">Na folha de saudação, clique em Olá **trocar** botão.</span><span class="sxs-lookup"><span data-stu-id="47f93-131">In hello blade, click hello **Swap** button.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="47f93-133">Olá seguinte prompt de confirmação é aberto.</span><span class="sxs-lookup"><span data-stu-id="47f93-133">hello following confirmation prompt opens.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="47f93-135">Depois de verificar as informações de implantação de saudação, clique em **Okey** tooswap implantações de saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="47f93-136">troca de implantação Olá rapidamente acontece porque Olá única alteração é Olá virtual VIPs (endereços IP) para implantações de saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="47f93-137">custos de computação toosave, você pode excluir Olá implantação de preparo depois de verificar se sua implantação de produção está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="47f93-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="47f93-138">Perguntas comuns sobre troca de implantações</span><span class="sxs-lookup"><span data-stu-id="47f93-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="47f93-139">**Quais são os pré-requisitos de saudação para implantações de permuta?**</span><span class="sxs-lookup"><span data-stu-id="47f93-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="47f93-140">Existem dois pré-requisitos essenciais para uma troca de implantação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="47f93-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="47f93-141">Se você quiser toouse um endereço IP estático para o slot de produção, você deve reservar um para o slot de preparo também.</span><span class="sxs-lookup"><span data-stu-id="47f93-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="47f93-142">Caso contrário, a troca de saudação falhará.</span><span class="sxs-lookup"><span data-stu-id="47f93-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="47f93-143">Todas as instâncias de funções de devem ser executado antes que você pode executar uma permuta de saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="47f93-144">Você pode verificar o status de saudação de instâncias na folha de visão geral de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f93-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="47f93-145">Como alternativa, você pode usar o hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) comando no Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47f93-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="47f93-146">Observe que atualizações do sistema operacional convidado e operações de recuperação de serviço também pode causar a implantação troca toofail.</span><span class="sxs-lookup"><span data-stu-id="47f93-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="47f93-147">Para saber mais, confira [Solucionar problemas de implantação do serviço de nuvem](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="47f93-148">**Uma troca incorre em tempo de inatividade para meu aplicativo? Como devo lidar com isso?**</span><span class="sxs-lookup"><span data-stu-id="47f93-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="47f93-149">Conforme descrito na seção de última Olá, uma troca de implantação é normalmente rápida, pois ela é apenas uma alteração de configuração no balanceador de carga do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="47f93-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="47f93-150">Entretanto, em alguns casos, ela pode levar dez segundos ou mais e resultar em falhas de conexão transitórias.</span><span class="sxs-lookup"><span data-stu-id="47f93-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="47f93-151">clientes de tooyour do impacto toolimit, considere implementar [lógica de repetição do cliente](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="47f93-152">Como: vincular a um serviço de nuvem do recurso tooa</span><span class="sxs-lookup"><span data-stu-id="47f93-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="47f93-153">Olá portal do Azure não contém links para recursos juntos como atual portal clássico do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="47f93-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="47f93-154">Em vez disso, implantar recursos adicionais toohello mesmo grupo de recursos que está sendo usado por Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="47f93-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="47f93-155">Como excluir implantações e um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="47f93-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="47f93-156">Antes de poder excluir um serviço de nuvem, você deve excluir cada implantação existente.</span><span class="sxs-lookup"><span data-stu-id="47f93-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="47f93-157">custos de computação toosave, você pode excluir Olá implantação de preparo depois de verificar se sua implantação de produção está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="47f93-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="47f93-158">Você será cobrado por custos de computação de instâncias de função implantadas que estejam paradas.</span><span class="sxs-lookup"><span data-stu-id="47f93-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="47f93-159">Use Olá toodelete do procedimento a seguir, uma implantação ou o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="47f93-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="47f93-160">Em Olá [portal do Azure][Azure portal], selecione Serviço de nuvem Olá toodelete desejado.</span><span class="sxs-lookup"><span data-stu-id="47f93-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="47f93-161">Essa etapa abre a folha de instância de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="47f93-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="47f93-162">Na folha de saudação, clique em Olá **excluir** botão.</span><span class="sxs-lookup"><span data-stu-id="47f93-162">In hello blade, click hello **Delete** button.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="47f93-164">Você pode excluir o serviço de nuvem inteira Olá verificando **serviços de nuvem e suas implantações** ou escolha a saudação **implantação de produção** ou hello **implantação de preparo**.</span><span class="sxs-lookup"><span data-stu-id="47f93-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="47f93-166">Clique em Olá **excluir** botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="47f93-167">serviço de nuvem Olá toodelete, clique em **excluir serviço de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="47f93-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="47f93-168">Em seguida, no prompt de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="47f93-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="47f93-169">Quando um serviço de nuvem é excluído e o monitoramento detalhado está configurado, você deve excluir manualmente dados saudação da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="47f93-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="47f93-170">Para obter informações sobre onde toofind Olá tabelas de métricas, consulte [isso](cloud-services-how-to-monitor.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="47f93-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="47f93-171">Como localizar mais informações sobre implantações com falha</span><span class="sxs-lookup"><span data-stu-id="47f93-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="47f93-172">Olá **visão geral** folha tem uma barra de status na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="47f93-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="47f93-173">Quando você clica em barras hello, uma nova folha abre e exibe informações de erro.</span><span class="sxs-lookup"><span data-stu-id="47f93-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="47f93-174">Se a implantação de saudação não contém quaisquer erros, folha de informações de saudação está em branco.</span><span class="sxs-lookup"><span data-stu-id="47f93-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="47f93-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47f93-176">Next steps</span></span>
* <span data-ttu-id="47f93-177">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="47f93-178">Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="47f93-179">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="47f93-180">Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47f93-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
