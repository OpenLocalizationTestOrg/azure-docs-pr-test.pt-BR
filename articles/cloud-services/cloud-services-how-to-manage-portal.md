---
title: "Tarefas comuns de gerenciamento de serviço de nuvem | Microsoft Docs"
description: "Saiba como gerenciar serviços de nuvem no portal do Azure. Esses exemplos usam o portal do Azure."
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
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="05ebe-104">Como gerenciar serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="05ebe-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05ebe-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="05ebe-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="05ebe-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="05ebe-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="05ebe-107">Na área **Serviços de Nuvem (clássico)** do Portal do Azure, você pode atualizar uma função de serviço ou uma implantação, promover uma implantação de preparo para produção, vincular recursos ao Serviço de Nuvem para que você possa ver as dependências de recursos e dimensionar os recursos em conjunto, além de excluir um Serviço de Nuvem ou uma implantação.</span><span class="sxs-lookup"><span data-stu-id="05ebe-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="05ebe-108">Obtenha mais informações sobre como dimensionar seu serviço de nuvem [aqui](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="05ebe-109">Como atualizar uma função ou implantação de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="05ebe-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="05ebe-110">Se você precisar atualizar o código do aplicativo para o seu serviço de nuvem, use **Atualizar** na folha do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="05ebe-111">Você pode atualizar única função ou todas as funções.</span><span class="sxs-lookup"><span data-stu-id="05ebe-111">You can update a single role or all roles.</span></span> <span data-ttu-id="05ebe-112">Para atualizar, você pode carregar um novo pacote de serviços ou o arquivo de configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="05ebe-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="05ebe-113">No [Portal do Azure][Azure portal], selecione o serviço de nuvem que você deseja atualizar.</span><span class="sxs-lookup"><span data-stu-id="05ebe-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="05ebe-114">Esta etapa abrirá a folha da instância do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="05ebe-115">Na folha, clique no botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="05ebe-115">In the blade, click the **Update** button.</span></span>

    ![Botão Atualizar](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="05ebe-117">Atualize a implantação com um novo arquivo de pacote de serviço (.cspkg) e o arquivo de configuração de serviço (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="05ebe-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="05ebe-119">**Como opção** , atualize o rótulo de implantação e a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05ebe-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="05ebe-120">Se alguma das funções tiver uma instância de função, selecione **Implantar mesmo se uma ou mais funções contiverem uma única instância** para permitir que a atualização continue.</span><span class="sxs-lookup"><span data-stu-id="05ebe-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="05ebe-121">O Azure pode garantir apenas 99,95 por cento de disponibilidade do Serviço de Nuvem durante uma atualização do Serviço de Nuvem se cada função tiver pelo menos duas instâncias de função (máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="05ebe-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="05ebe-122">Com duas instâncias de função, uma máquina virtual processa as solicitações do cliente enquanto a outra é atualizada.</span><span class="sxs-lookup"><span data-stu-id="05ebe-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="05ebe-123">Marque a opção **Iniciar implantação** para que a atualização seja aplicada após terminar o upload do pacote.</span><span class="sxs-lookup"><span data-stu-id="05ebe-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="05ebe-124">Clique em **OK** para iniciar a atualização do serviço.</span><span class="sxs-lookup"><span data-stu-id="05ebe-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="05ebe-125">Como permutar implantações para promover a implantação de preparo para produção</span><span class="sxs-lookup"><span data-stu-id="05ebe-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="05ebe-126">Ao optar por implantar uma nova versão do serviço de nuvem, prepare e teste a nova versão em seu ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="05ebe-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="05ebe-127">Use **Permutar** para alternar as URLs pelas quais as duas implantações são endereçadas e para promover uma nova versão para produção.</span><span class="sxs-lookup"><span data-stu-id="05ebe-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="05ebe-128">É possível permutar implantações na página **Serviços de Nuvem** ou no painel.</span><span class="sxs-lookup"><span data-stu-id="05ebe-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="05ebe-129">No [Portal do Azure][Azure portal], selecione o serviço de nuvem que você deseja atualizar.</span><span class="sxs-lookup"><span data-stu-id="05ebe-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="05ebe-130">Esta etapa abrirá a folha da instância do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="05ebe-131">Na folha, clique o botão **Trocar** .</span><span class="sxs-lookup"><span data-stu-id="05ebe-131">In the blade, click the **Swap** button.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="05ebe-133">O seguinte aviso de confirmação é aberto.</span><span class="sxs-lookup"><span data-stu-id="05ebe-133">The following confirmation prompt opens.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="05ebe-135">Após verificar as informações da implantação, clique em **OK** para trocar as implantações.</span><span class="sxs-lookup"><span data-stu-id="05ebe-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="05ebe-136">A permuta da implantação acontece rapidamente pois a única coisa alterada são os endereços IP virtuais (VIP) para as implantações.</span><span class="sxs-lookup"><span data-stu-id="05ebe-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="05ebe-137">Para economizar custos de computação, você pode excluir a implantação de preparo após verificar que sua implantação de produção está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="05ebe-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="05ebe-138">Perguntas comuns sobre troca de implantações</span><span class="sxs-lookup"><span data-stu-id="05ebe-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="05ebe-139">**Quais são os pré-requisitos para a troca de implantações?**</span><span class="sxs-lookup"><span data-stu-id="05ebe-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="05ebe-140">Existem dois pré-requisitos essenciais para uma troca de implantação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="05ebe-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="05ebe-141">Se quiser usar um endereço IP estático para o slot de produção, você também deverá reservar um para o slot de preparo.</span><span class="sxs-lookup"><span data-stu-id="05ebe-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="05ebe-142">Caso contrário, a troca falhará.</span><span class="sxs-lookup"><span data-stu-id="05ebe-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="05ebe-143">Todas as instâncias de suas funções devem estar em execução para que você possa executar a troca.</span><span class="sxs-lookup"><span data-stu-id="05ebe-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="05ebe-144">Você pode verificar o status de suas instâncias na folha Visão geral do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="05ebe-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="05ebe-145">Como alternativa, use o comando [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) no Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05ebe-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="05ebe-146">Observe que as atualizações do SO convidado e as operações de recuperação de serviço também podem fazer com que as trocas de implantação falhem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="05ebe-147">Para saber mais, confira [Solucionar problemas de implantação do serviço de nuvem](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="05ebe-148">**Uma troca incorre em tempo de inatividade para meu aplicativo? Como devo lidar com isso?**</span><span class="sxs-lookup"><span data-stu-id="05ebe-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="05ebe-149">Conforme descrito na última seção, uma troca de implantação normalmente é rápida, pois é apenas uma alteração de configuração no Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="05ebe-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="05ebe-150">Entretanto, em alguns casos, ela pode levar dez segundos ou mais e resultar em falhas de conexão transitórias.</span><span class="sxs-lookup"><span data-stu-id="05ebe-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="05ebe-151">Para limitar o impacto sobre os clientes, considere a implementação da [lógica de repetição do cliente](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="05ebe-152">Como vincular um recurso a um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="05ebe-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="05ebe-153">O portal do Azure não vinculada recursos como o portal clássico do Azure atual.</span><span class="sxs-lookup"><span data-stu-id="05ebe-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="05ebe-154">Em vez disso, implante recursos adicionais para o mesmo grupo de recursos que está sendo usado pelo Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="05ebe-155">Como excluir implantações e um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="05ebe-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="05ebe-156">Antes de poder excluir um serviço de nuvem, você deve excluir cada implantação existente.</span><span class="sxs-lookup"><span data-stu-id="05ebe-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="05ebe-157">Para economizar custos de computação, você pode excluir a implantação de preparo após verificar que sua implantação de produção está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="05ebe-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="05ebe-158">Você será cobrado por custos de computação de instâncias de função implantadas que estejam paradas.</span><span class="sxs-lookup"><span data-stu-id="05ebe-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="05ebe-159">Use o procedimento a seguir para excluir uma implantação ou seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="05ebe-160">No [Portal do Azure][Azure portal], selecione o serviço de nuvem que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="05ebe-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="05ebe-161">Esta etapa abrirá a folha da instância do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ebe-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="05ebe-162">Na folha, clique no botão **Excluir** .</span><span class="sxs-lookup"><span data-stu-id="05ebe-162">In the blade, click the **Delete** button.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="05ebe-164">Você pode excluir o serviço de nuvem inteiro marcando **Serviços de nuvem e suas implantações** ou escolhendo **Implantação de produção** ou **Implantação de preparo**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="05ebe-166">Clique no botão **Excluir** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="05ebe-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="05ebe-167">Para excluir o Serviço de Nuvem, clique em **Excluir o Serviço de Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="05ebe-168">Em seguida, clique em **Sim**no prompt de confirmação.</span><span class="sxs-lookup"><span data-stu-id="05ebe-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="05ebe-169">Quando um serviço de nuvem for excluído, e o monitoramento detalhado estiver configurado, você deverá excluir manualmente os dados de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05ebe-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="05ebe-170">Para obter informações sobre onde encontrar as tabelas de métricas, consulte [este](cloud-services-how-to-monitor.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="05ebe-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="05ebe-171">Como localizar mais informações sobre implantações com falha</span><span class="sxs-lookup"><span data-stu-id="05ebe-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="05ebe-172">A folha **Visão geral** tem uma barra de status na parte superior.</span><span class="sxs-lookup"><span data-stu-id="05ebe-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="05ebe-173">Quando você clica na barra, uma nova folha é aberta e exibe informações de erro.</span><span class="sxs-lookup"><span data-stu-id="05ebe-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="05ebe-174">Se a implantação não contiver erros, a folha de informações ficará em branco.</span><span class="sxs-lookup"><span data-stu-id="05ebe-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="05ebe-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05ebe-176">Next steps</span></span>
* <span data-ttu-id="05ebe-177">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="05ebe-178">Saiba como [implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="05ebe-179">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="05ebe-180">Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
